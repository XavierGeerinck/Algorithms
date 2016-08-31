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

The top down method has been recommended by the creators of this algorithm, because it is faster then the bottom-up version. When going down we will put all the nodes on this path out of the way, and we will perform rotations to keep our atomaire operations.

How it works is that we have 3 subtrees called L, R and M. L contains the keys that are < than the keys in M and R contains the keys that are > than the keys in M. We start with L and R empty and M with our whole subtree. Now we can split our trees as shown in the cases below.

| Zig Case | Zig Zig Case |
| --- | --- |
| ![](/images/datastructures/splay_top_down_zig_case.png) | ![](/images/datastructures/splay_top_down_zig_zig_case.png) |
| Zig Zag Case |  |
| ![](/images/datastructures/splay_top_down_zig_zag_case.png) |  |

Once we are down, the only thing left to do is to merge the M, L and R subtrees back together with root C.

![](/images/datastructures/splay_top_down_merge.png)