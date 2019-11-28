# obj2mesh
Simple terminal converter from 'obj' to 'mesh' format. Mesh is custom binary format designed for easy use with OpenGL API and loaded content could be directly passed to GPU VRAM.

## Compilation
```bash
blc obj2mesh.bl
```

## Data representation
* Color - stored as `v4` type.
* Vertex - stored as `v3` type.
* Normal - stored as `v3` type.
* UV - stored as `v2` type.
* Index - stored as `u32` type.

## Change log
* 1.0.0 - Initial release.
