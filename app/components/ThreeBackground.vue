<template>
  <canvas ref="canvasRef" class="three-bg-canvas" />
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted, ref } from 'vue'

const canvasRef = ref<HTMLCanvasElement | null>(null)
let animId: number | null = null
let cleanupFns: (() => void)[] = []

onMounted(async () => {
  if (window.innerWidth <= 768) return

  const THREE = await import('three')

  const canvas = canvasRef.value!
  const renderer = new THREE.WebGLRenderer({ canvas, antialias: true })
  renderer.setSize(window.innerWidth, window.innerHeight)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  renderer.toneMapping = THREE.ACESFilmicToneMapping
  renderer.toneMappingExposure = 1.0
  renderer.setClearColor(0xe8e6e1, 1)

  const scene = new THREE.Scene()
  const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 100)
  camera.position.set(0, 0, 5)

  // Lighting
  const ambient = new THREE.AmbientLight(0xffffff, 0.5)
  scene.add(ambient)

  const key = new THREE.DirectionalLight(0xffffff, 2.8)
  key.position.set(5, 6, 5)
  scene.add(key)

  const fill = new THREE.DirectionalLight(0x8899ff, 1.2)
  fill.position.set(-4, 2, -3)
  scene.add(fill)

  const rim = new THREE.DirectionalLight(0xffd0a0, 0.8)
  rim.position.set(0, -4, 3)
  scene.add(rim)

  // Crystal group
  const group = new THREE.Group()
  scene.add(group)

  // Solid low-poly crystal (flat shading = faceted gem look)
  const solidGeo = new THREE.IcosahedronGeometry(1.4, 1)
  const solidMat = new THREE.MeshStandardMaterial({
    color: 0xfafafa,
    metalness: 0.15,
    roughness: 0.65,
    flatShading: true,
  })
  const solidMesh = new THREE.Mesh(solidGeo, solidMat)
  group.add(solidMesh)

  // Edge lines for crystal facets
  const edgesGeo = new THREE.EdgesGeometry(new THREE.IcosahedronGeometry(1.42, 1))
  const edgesMat = new THREE.LineBasicMaterial({
    color: 0x6655cc,
    transparent: true,
    opacity: 0.28,
  })
  const edgeLines = new THREE.LineSegments(edgesGeo, edgesMat)
  group.add(edgeLines)

  // Outer glow wireframe shell
  const outerGeo = new THREE.IcosahedronGeometry(1.75, 0)
  const outerMat = new THREE.MeshBasicMaterial({
    color: 0x4433aa,
    wireframe: true,
    transparent: true,
    opacity: 0.07,
  })
  const outerMesh = new THREE.Mesh(outerGeo, outerMat)
  group.add(outerMesh)

  // Scroll sections — crystal journeys RIGHT → LEFT as user scrolls down
  // posX: positive = right side, negative = left side
  // ~3.5+ means partially off-screen (viewport half-width ≈ 4.3 at camZ=5)
  const sections = [
    { scrollStart: 0,    scrollEnd: 0.15, posX:  3.2, posY:  0.1,  rotX: 0,    rotY: 0,           camZ: 5.0, scale: 1.4  }, // Hero: right, partially cut off
    { scrollStart: 0.15, scrollEnd: 0.32, posX:  2.0, posY:  0.0,  rotX: 0.2,  rotY: 0.8,         camZ: 5.0, scale: 1.3  }, // About: right, fully visible
    { scrollStart: 0.32, scrollEnd: 0.50, posX:  1.0, posY: -0.1,  rotX: -0.2, rotY: 1.8,         camZ: 5.0, scale: 1.25 }, // Projects: center-right
    { scrollStart: 0.50, scrollEnd: 0.67, posX: -0.5, posY:  0.1,  rotX: 0.3,  rotY: 3.0,         camZ: 5.0, scale: 1.2  }, // Skills: crossing center to left
    { scrollStart: 0.67, scrollEnd: 0.83, posX: -2.0, posY:  0.0,  rotX: -0.1, rotY: 4.0,         camZ: 5.0, scale: 1.25 }, // Contact: left side
    { scrollStart: 0.83, scrollEnd: 1.0,  posX: -3.4, posY:  0.0,  rotX: 0.1,  rotY: Math.PI * 2, camZ: 5.0, scale: 1.3  }, // Footer: left, partially cut off
  ]

  function lerp(a: number, b: number, t: number) { return a + (b - a) * t }
  function smoothstep(a: number, b: number, t: number) {
    const x = Math.max(0, Math.min(1, (t - a) / (b - a)))
    return x * x * (3 - 2 * x)
  }

  let scrollProgress = 0
  let targetScrollProgress = 0

  // Drag-to-orbit
  let isDragging = false
  let dragStartX = 0, dragStartY = 0
  let orbitX = 0, orbitY = 0
  let targetOrbitX = 0, targetOrbitY = 0
  const DRAG_SENS = 0.005
  const ORBIT_DECAY = 0.035

  const onDown = (e: PointerEvent) => {
    isDragging = true
    dragStartX = e.clientX
    dragStartY = e.clientY
  }
  const onMove = (e: PointerEvent) => {
    if (!isDragging) return
    targetOrbitX = (e.clientX - dragStartX) * DRAG_SENS
    targetOrbitY = (e.clientY - dragStartY) * DRAG_SENS
  }
  const onUp = () => {
    isDragging = false
    dragStartX = 0; dragStartY = 0
  }
  const onScroll = () => {
    const h = document.documentElement.scrollHeight - window.innerHeight
    targetScrollProgress = h > 0 ? window.scrollY / h : 0
  }
  const onResize = () => {
    camera.aspect = window.innerWidth / window.innerHeight
    camera.updateProjectionMatrix()
    renderer.setSize(window.innerWidth, window.innerHeight)
  }

  window.addEventListener('pointerdown', onDown)
  window.addEventListener('pointermove', onMove)
  window.addEventListener('pointerup', onUp)
  window.addEventListener('scroll', onScroll)
  window.addEventListener('resize', onResize)

  cleanupFns.push(
    () => window.removeEventListener('pointerdown', onDown),
    () => window.removeEventListener('pointermove', onMove),
    () => window.removeEventListener('pointerup', onUp),
    () => window.removeEventListener('scroll', onScroll),
    () => window.removeEventListener('resize', onResize),
    () => { if (animId) cancelAnimationFrame(animId) },
    () => renderer.dispose(),
  )

  // Animation loop
  function animate() {
    animId = requestAnimationFrame(animate)
    scrollProgress += (targetScrollProgress - scrollProgress) * 0.055

    let cur = sections[0]
    let nxt = sections[1] || sections[0]
    let localT = 0

    for (let i = 0; i < sections.length; i++) {
      if (scrollProgress >= sections[i].scrollStart && scrollProgress <= sections[i].scrollEnd) {
        cur = sections[i]
        nxt = sections[Math.min(i + 1, sections.length - 1)]
        localT = smoothstep(cur.scrollStart, cur.scrollEnd, scrollProgress)
        break
      }
      if (i === sections.length - 1) { cur = nxt = sections[i]; localT = 1 }
    }

    const posX  = lerp(cur.posX,  nxt.posX,  localT)
    const posY  = lerp(cur.posY,  nxt.posY,  localT)
    const rotX  = lerp(cur.rotX,  nxt.rotX,  localT)
    const rotY  = lerp(cur.rotY,  nxt.rotY,  localT)
    const camZ  = lerp(cur.camZ,  nxt.camZ,  localT)
    const scale = lerp(cur.scale, nxt.scale, localT)

    if (isDragging) {
      orbitX += (targetOrbitX - orbitX) * 0.12
      orbitY += (targetOrbitY - orbitY) * 0.12
    } else {
      orbitX += (0 - orbitX) * ORBIT_DECAY
      orbitY += (0 - orbitY) * ORBIT_DECAY
      targetOrbitX += (0 - targetOrbitX) * ORBIT_DECAY
      targetOrbitY += (0 - targetOrbitY) * ORBIT_DECAY
    }

    group.position.x = posX
    group.position.y = posY
    group.rotation.x = rotX + orbitY
    group.rotation.y = rotY + Math.sin(Date.now() * 0.00035) * 0.06 + orbitX
    group.rotation.z = Math.sin(Date.now() * 0.00022) * 0.04
    group.scale.setScalar(scale)
    camera.position.z = camZ

    renderer.render(scene, camera)
  }

  animate()
})

onUnmounted(() => {
  cleanupFns.forEach(fn => fn())
})
</script>

<style scoped>
.three-bg-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 0;
  pointer-events: none;
  cursor: grab;
}

@media (max-width: 768px) {
  .three-bg-canvas {
    display: none;
  }
}
</style>
