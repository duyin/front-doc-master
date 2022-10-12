<template>
  <div class="mermaid">
    <slot></slot>
  </div>
</template>

<script>
export default {
  beforeMount() {
    import("mermaid/dist/mermaid").then(m => {
      m.initialize({
        startOnLoad: true,
        theme: 'forest'
      });
      m.init();
    });
  }
};
</script>