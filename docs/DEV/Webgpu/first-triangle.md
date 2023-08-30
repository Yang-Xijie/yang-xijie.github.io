# First Triangle

Codes from <https://developer.chrome.com/blog/webgpu-io2023/>.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>first triangle on-screen</title>
  </head>
  <body>
    <canvas id="canvas" width="512" height="512"></canvas>
    <script type="module">
      const adapter = await navigator.gpu.requestAdapter();
      const device = await adapter.requestDevice();

      const context = canvas.getContext("webgpu");
      const format = navigator.gpu.getPreferredCanvasFormat();
      context.configure({ device, format });

      const code = `
    @vertex fn vertexMain(@builtin(vertex_index) i : u32) ->
      @builtin(position) vec4f {
       const pos = array(vec2f(0, 1), vec2f(-1, -1), vec2f(1, -1));
       return vec4f(pos[i], 0, 1);
    }
    @fragment fn fragmentMain() -> @location(0) vec4f {
      return vec4f(1, 0, 0, 1);
    }`;
      const shaderModule = device.createShaderModule({ code });
      const pipeline = device.createRenderPipeline({
        layout: "auto",
        vertex: {
          module: shaderModule,
          entryPoint: "vertexMain",
        },
        fragment: {
          module: shaderModule,
          entryPoint: "fragmentMain",
          targets: [{ format }],
        },
      });
      const commandEncoder = device.createCommandEncoder();
      const colorAttachments = [
        {
          view: context.getCurrentTexture().createView(),
          loadOp: "clear",
          storeOp: "store",
        },
      ];
      const passEncoder = commandEncoder.beginRenderPass({ colorAttachments });
      passEncoder.setPipeline(pipeline);
      passEncoder.draw(3);
      passEncoder.end();
      device.queue.submit([commandEncoder.finish()]);
    </script>
  </body>
</html>
```
