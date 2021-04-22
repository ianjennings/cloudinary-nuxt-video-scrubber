<template>
  <div>
    <h1>Hello, world!</h1>

    <cld-image cloudName="demo" publicId="sample" crop="scale" width="300" />

    <cld-context cloudName="demo">
      <cld-image publicId="sample">
        <cld-transformation crop="scale" width="200" angle="10" />
      </cld-image>
    </cld-context>
  </div>
</template>
