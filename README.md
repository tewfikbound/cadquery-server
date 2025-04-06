import cadquery as cq

# Dimensions
diameter = 40  # mm
height = 29  # mm

boss_length = 20  # mm
boss_width = 13  # mm
boss_height = 5  # mm

thread_diameter = 12  # mm (M12)

# Main cylindrical body
part = cq.Workplane("XY").circle(diameter / 2).extrude(height)

# Add the boss
boss = (
    cq.Workplane("XY")
    .workplane(offset=height)
    .center(0, 0)
    .rect(boss_length, boss_width)
    .extrude(boss_height)
)

part = part.union(boss)

# Add simple hole
part = part.faces(">Z").workplane().hole(thread_diameter)

show_object(part)
