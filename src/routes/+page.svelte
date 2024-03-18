<script lang="ts">
  import Cropper from 'cropperjs';
  // IMPORTANT! This import required for CropperJS to work properly
  import 'cropperjs/dist/cropper.css';
	import { onDestroy, onMount } from 'svelte';

  let cropper: Cropper;
  let img: HTMLImageElement;

  const initCropper = () => {
    cropper = new Cropper(img, {
      aspectRatio: 1,
      cropBoxMovable: false,
      cropBoxResizable: false,
      toggleDragModeOnDblclick: false,
      dragMode: 'move',
      rotatable: true,
      viewMode: 1,
      crop: () => {
        console.log('cropped');
      },
    });
  };

  onMount(() => {
    if (img.complete) {
      initCropper()
    } else {
      img.addEventListener('load', () => initCropper(), { once: true });
    }
  });

  onDestroy(() => cropper?.destroy());
</script>

<h1>SvelteKit with CropperJS Demo</h1>

<div class="cropper-container">
  <img bind:this={img} src="/images/face.jpg" alt="a persons's face" />
</div>

<style>
  .cropper-container {
    width: 800px;
    height: 400px;
  }

  img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
</style>