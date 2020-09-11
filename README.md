# transform_graph

- [ROS wiki](https://wiki.ros.org/transform_graph)
- [Code API](https://docs.ros.org/indigo/api/transform_graph/html/)

`transform_graph` is a library that computes transformations betweens arbitrary frames in a graph of transformations.
See the generated documentation for details.

Basic example:
```cpp
#include "transform_graph/transform_graph.h"

transform_graph::Graph graph;
graph.Add("wrist", transform_graph::RefFrame("base_link"), wrist_pose_stamped);
graph.Add("kinect", transform_graph::RefFrame("base_link"), kinect_pose_stamped);

// Find out if a point in the frame of the Kinect is near the wrist.
pcl::PointXYZ point_in_kinect = ...;
transform_graph::Position point_in_wrist;
graph.DescribePosition(point_in_kinect, transform_graph::Source("kinect"), transform_graph::Target("wrist"), &point_in_wrist);
if (point_in_wrist.vector().norm() < 0.05) {
  ...
}
```
