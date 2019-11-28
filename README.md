# obj2mesh
Simple terminal converter from 'obj' to 'mesh' format. Mesh is custom binary format designed for easy use with OpenGL API and loaded content could be directly passed to GPU VRAM.

## Compilation
```bash
blc obj2mesh.bl
```

## Usage
```bash
./obj2mesh <obj-files>
```

## Data representation
* Color - stored as `v4` type.
* Vertex - stored as `v3` type.
* Normal - stored as `v3` type.
* UV - stored as `v2` type.
* Index - stored as `u32` type.

## API Load example
```
#load "std/print.bl"
#load "o2m_loader.bl"

MyMesh :: struct {
    v: []v3;
    data: O2M_Mesh;
}

mesh := {:MyMesh: 0};

main :: fn () {
    // Load 'model.mesh' from file.
    e := o2m_load(&mesh.data, "model.mesh");
    if e != O2M_Error.NoError { panic(); }
    
    // Free loaded data.
    defer o2m_free(mesh.data);
    
    // Map vertex data to 'mesh.v'.
    e = o2m_get_elem_count(auto &mesh.v.len, mesh.data, O2M_Elem.Vertex);
    if e != O2M_Error.NoError { panic(); }
    
    if mesh.v.len > 0 {
        e = o2m_get_elem_ptr(auto &mesh.v.ptr, mesh.data, O2M_Elem.Vertex);
        if e != O2M_Error.NoError { panic(); }
    }
    
    loop i := 0; i < mesh.v.len; i += 1 {
        print("%", mesh.v[i]);
    }
}
```

## Change log
* 1.0.0 - Initial release.
