<template>
  <div>
    <h1>Hello, world!</h1>

    <cld-video cloudName="demo" publicId="dog" controls="true">
      <cld-transformation width="0.4" angle="20" />
      <cld-transformation
        overlay="cloudinary_icon_white"
        width="60"
        opacity="50"
        gravity="south_east"
        y="15"
        x="60"
      />
    </cld-video>
  </div>
</template>
