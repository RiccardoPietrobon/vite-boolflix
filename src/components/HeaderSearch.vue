<script>

export default {
  data() {
    return {
      title: "Header",
    }
  }

  // components: {
  //   MyComponent,
  // },
};
</script>

<template>
  <div class="bg-dark">

    <div class="header d-flex container p-5">
      <h1 class="text-danger">BOOLFLIX</h1>
      <div class="input-group input-group-sm">
        <input type="text" class="form-control" placeholder="Recipient's username"
          aria-label="Recipient's username with two button addons" aria-describedby="inputGroup-sizing-sm">
        <button class="btn btn-outline-secondary" type="button">Button</button>
        <button class="btn btn-outline-secondary" type="button">Button</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
