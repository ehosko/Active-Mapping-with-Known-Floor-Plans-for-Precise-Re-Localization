# Active-Mapping-with-Known-Floor-Plans-for-Precise-Re-Localization

[Report](./docs/Report.pdf)

Cutting-edge devices like augmented reality headsets or micro aerial vehicles require
precise localization to complete a variety of tasks. An approach to enable an agent
to localize itself in a particular area is to first create a map and then re-localize
itself in the created map. The autonomous creation of such maps is a non-trivial
and widely researched problem. The numerous active exploration and mapping
approaches may pursue different objectives, such as accurate 3D reconstruction,
surface inspection, or the aforementioned localization, but often share a framework
structure.
Many traditional approaches do not consider any prior information. However, in
real-world scenarios, 2D floor plans are widely available and can be used to influence
the decision of the planner with the information at hand.
This project aims to implement an exploration planner that maps an environment
with the goal of precise re-localization. To that end, the frequent availability of
2D floor plans is exploited for a more informed exploration and mapping process.
A novel exploration planner is introduced in four variants trying to revisit drifty
regions during the mapping process to increase the localization ability.
The four variants of the proposed planner are compared against three different planners
using a custom evaluation framework quantifying the re-localization accuracy
of the created map. Further analysis is conducted regarding the precision of pose
estimation during the mapping process and the efficiency of the exploration. The
analysis shows that the novel exploration planner improves the re-localization accuracy
compared to the other planners. However, the prior information gained from
the 2D floor plan could not be exploited to its full potential.

## Components
- [Exploration Planner and main framework structure](https://github.com/ehosko/optimal_active_guidance_in_mixed_reality_using_prior_floorplans)
- [SLAM system](https://github.com/ehosko/maplab)
- [Floor Plan Inclusion](https://github.com/ehosko/localization_using_floorplans)
- [Evaluation](https://github.com/ehosko/rpg_trajectory_evaluation) 
