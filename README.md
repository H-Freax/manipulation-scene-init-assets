# manipulation-scene-init-assets

PyBullet robot + clutter assets for the SkillsBench task
[`manipulation-scene-init`](https://github.com/benchflow-ai/skillsbench/pull/857).

The task is a robotics scene-setup benchmark that asks an agent to build a
PyBullet scene from a spec — load the arm (UR5e + a separate Robotiq 2F-85
gripper, or a Franka Panda with an integrated hand), drop a clutter of
objects into a stable pile, and add an RGB-D camera. This repo holds
everything needed to load those scenes; the task's `Dockerfile` clones it
at a pinned commit during the image build so the SkillsBench PR itself
stays small.

## Layout

| Subtree | Description |
|---|---|
| `clutter/<id>/` | 33 tabletop objects (visual mesh + V-HACD convex collision + ready `object.urdf`) |
| `ur5e/` | UR5e 6-DOF arm URDF + meshes |
| `robotiq/` | Robotiq 2F-85 parallel-jaw gripper URDF + meshes |
| `franka_panda/` | Franka Panda 7-DOF arm with integrated hand |
| `workspace/` | Floor + table-frame URDFs and visual meshes |

See [`PROVENANCE.md`](PROVENANCE.md) for full upstream attribution
(ThinkGrasp, CoRL 2024, MIT) and a per-subtree mapping back to the
upstream paths. The byte-pinning of every asset file is recorded in
[`CHECKSUMS.sha256`](CHECKSUMS.sha256) and can be verified with:

```bash
shasum -a 256 -c CHECKSUMS.sha256
```

Line endings are preserved as-is (`.gitattributes` marks every file
`-text`), so the recorded hashes stay valid across clones on any platform.

## License

[MIT](LICENSE) — matching the upstream license of the assets.
