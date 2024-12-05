# Detailed explanation and clarification  
## What is Octrees?什么是八叉树？  
  It is a spatial segmentation data structure widely used in tasks such as object management, collision detection, and rendering optimization in 3D space.  
  It divides the three-dimensional space into eight sub regions and refines the space recursively.  
  八叉树是一种空间分割的数据结构，它被广泛应用于 3D 空间中的物体管理、碰撞检测、渲染优化等任务。它将三维空间划分成八个子区域，通过递归方式对空间进行细化。  
## Base structure 八叉树基本结构  
  包含三种重要的节点  
  ·Root Node根节点：表示空间的整个范围（例如可以是一个立方体的边界框）  
  ·Child Node子节点：将父节点的空间进一步划分成八个子区域，每个子区域代表一个子立方体，然后再依次进行递归  
  ·Leaf Node叶节点：表示最终存储数据的区域，通常存储物体、碰撞体、或者其他三维的数据  
  进一步地，八叉树中，每个节点存储当前区域的坐标范围、它的子节点、物体的列表（如果有物体在该空间中）  
## Implementation ideas 八叉树的实现思路  
  ### ·定义节点类  
    每一个节点应该表示一个空间区域，它包含一个三维坐标下的空间范围（这个范围可以自己设定）和可能的物体列表  
    同时，每一个节点可以包含8个子节点，这些子节点表示的是子空间的划分  
  ### ·递归地再划分空间  
    通过递归将空间不断划为8个子区域，直到达到设定的最小分割范围或者每一个节点区域内存储的物体数达到了阈值  
  ### ·插入物体  
    当需要插入物体时，根据它的位置和空间范围判断属于哪个区域  
    如果当前区域已经划分为子区域，则将物体插入相应的子节点，否则将物体直接插入当前节点
  ### ·查询和更新  
    查询：根据物体的位置快速查找它所在的区域  
    更新：根据物体的位置的变化，重新插入物体或者更新八叉树的结构  
## Main application scenarios 主要应用场景  
  碰撞检测、视锥体剔除（可以快速确定哪些物体在相机视锥体内，哪些在外，从而渲染不必要的物体）、AI的行为决策、地图的管理  
## A-star pathfinding algorithm A星寻路算法  
  https://github.com/shantouly/Astar该篇有介绍A星寻路，也有demo  
## Application of Octree Combined with A-star Routing Algorithm 八叉树结合AStar  
  In 3D space, the efficiency of A * decreases as the complexity of the space increases.  
  In this case, introducing an octree can significantly improve the performance of Astar  
  在3D空间中，A*的效率会随着空间的复杂度的增加而下降，此时，引入八叉树可以使得Astar的性能得到显著的提升  
## Algorithm steps 算法的步骤  
  ### ·构建八叉树  
  ### ·A*初始化（确定起始和终点）  
  ### ·FindPath （网格的节点即为构建八叉树时候将空间分割的那些节点）将起点放进关闭列表，遍历周围子节点，计算代价，放进关闭，重复......  
  ### ·回溯路径 寻找到终点之后，遍历父节点直到父节点为null  
  ### ·动态更新八叉树 当物体从某个区域换成另一个区域时，需要重新计算八叉树，然后重新进行路径的计算  
  
  
  
