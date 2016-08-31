# Splay Trees

Splay Trees are kind of special when it comes to how they work performance wise. They just as Red-Black trees have a performance of O\(log\(n\)\) but it accomplishes this by looking at m operations and making these O\(m log\(n\)\).

## Bottom Up

The bottom up method uses a term called _splaying_, this will set a specific element as the root element through rotations. This splaying method can be explained with three specific cases:

| Zig Case | Zig Zag Case |
| --- | --- |
| Rotate Right over P ![](/images/datastructures/splay_bottom_up_zig_case.png) | First rotate C left over P and then rotate this solution right over G ![](/images/datastructures/splay_bottom_up_zig_zag_case.png) |
| Zig Zig Case |  |
| First rotate C over P right and then again rotate right over G ![](/images/datastructures/splay_bottom_up_zig_zig_case.png) |  |

## Top Down

| Zig Case | Zig Zig Case |
| --- | --- |
| ![](/images/datastructures/splay_top_down_zig_case.png) | ![](/images/datastructures/splay_top_down_zig_zig_case.png) |
| Zig Zag Case |  |
| ![](/images/datastructures/splay_top_down_zig_zag_case.png) |  |

