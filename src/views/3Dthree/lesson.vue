<template>
  <div class="threeBox">
    <canvas id="three" style=" width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
"></canvas>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-class-component'
import * as THREE from 'three'
import CameraControls from 'camera-controls';

export default class Home extends Vue {
  public mounted () {
    /**
     * 创建场景对象Scene
     */
    var scene = new THREE.Scene();
    /**
     * 创建网格模型
     */
    // var geometry = new THREE.SphereGeometry(60, 40, 40); // 创建一个球体几何对象
    var geometry = new THREE.BoxGeometry(100, 100, 100); // 创建一个立方体几何对象Geometry
    // var material = new THREE.MeshLambertMaterial({
    //   color: 0x33ccff,
    //   opacity: 0.3,
    //   wireframe: true,
    //   transparent: true
    // }); // 材质对象Material
    var sphereMaterial = new THREE.MeshPhongMaterial({
      color: 0x33ccff,
      specular: 0x4488ee,
      shininess: 12,
      opacity: 0.3
      // wireframe: true
      // transparent: true
    });// 材质对象
    var mesh = new THREE.Mesh(geometry, sphereMaterial); // 网格模型对象Mesh
    scene.add(mesh); // 网格模型添加到场景中
    /**
     * 光源设置
     */
    // 点光源
    var point = new THREE.PointLight(0xffffff);
    point.position.set(400, 180, 300); // 点光源位置
    scene.add(point); // 点光源添加到场景中

    var point1 = new THREE.PointLight(0xffffff);
    point1.position.set(-200, 580, -150); // 点光源位置
    scene.add(point1); // 点光源添加到场景中
    // 环境光
    var ambient = new THREE.AmbientLight(0x000000);
    scene.add(ambient);
    // console.log(scene)
    // console.log(scene.children)
    /**
     * 相机设置
     */
    var width = window.innerWidth; // 窗口宽度
    var height = window.innerHeight; // 窗口高度
    var k = width / height; // 窗口宽高比
    var s = 100; // 三维场景显示范围控制系数，系数越大，显示的范围越大
    // 创建相机对象
    var camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 500);
    camera.position.set(200, 300, 200); // 设置相机位置
    camera.lookAt(scene.position); // 设置相机方向(指向的场景对象)
    /**
     * 创建渲染器对象
     */
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(width, height);// 设置渲染区域尺寸
    renderer.setClearColor(0xb9d3ff, 1); // 设置背景颜色
    document.body.appendChild(renderer.domElement); // body元素中插入canvas对象
    // 执行渲染操作   指定场景、相机作为参数
    renderer.render(scene, camera);

    function render () {
      renderer.render(scene, camera);// 执行渲染操作
      mesh.rotateY(0.01);// 每次绕y轴旋转0.01弧度
      requestAnimationFrame(render);// 请求再次执行渲染函数render
    }
    render();
    CameraControls.install({ THREE: THREE });
    const cameraControls = new CameraControls(camera, renderer.domElement);
    cameraControls.addEventListener('control', render);

    // controls.addEventListener('change', render);// 监听鼠标、键盘事件
  }
}
</script>

<style>

</style>
