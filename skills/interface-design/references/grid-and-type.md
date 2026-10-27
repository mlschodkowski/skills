> Reference guidance. The parent skill controls scope and mode. Follow the
> current product and platform; verify version-sensitive API details when used.

# Swiss Design

Make content, relationships, and actions clear through deliberate structure.
Combine Swiss composition with the precision of Vercel's Geist system.

Respect the product's established identity. Apply this direction when requested
or when the project already uses it. Preserve native platform conventions.

## Start with the content

Identify the person's task, the primary information, and the next action.
Group related content. Separate what people must read, compare, and control.

Choose the structure before the styling. Each visual distinction should express
importance, grouping, state, action, or depth.

## Apply the visual language within the product

Inspect existing components, tokens, routing, and state handling first.
Preserve their contracts while changing presentation.

Keep the product's domain and vocabulary. Use real tasks and content to
shape the screen. Operational tools need working controls, useful density,
and clear metadata.

Reuse project tokens. If none exist, define a small semantic token set
before repeating raw values. Use the same role names across themes.

## Compose with a grid

Use shared alignment lines, consistent gutters, and deliberate content widths.
Derive columns from the content and its minimum readable size.

Use asymmetry when it creates useful emphasis. Balance it through alignment,
proportion, and space.

Keep reading order coherent as columns collapse. Let long labels, translations,
large text, and real data determine where the layout must adapt.

Visible grid lines are an optional graphic treatment. Use them when the cell
structure contributes to the composition. Use ordinary layout primitives when
alignment alone does the work.

## Build with typography

Define text roles for headings, body copy, labels, and technical information.
Give each role a consistent size, weight, line height, and tracking.

Use a readable sans serif for general interface text. Geist Sans is a suitable
choice when the project permits it. Use existing fonts when Geist is unavailable.
Use monospace for code and identifiers. Use tabular numerals where changing
numbers must remain aligned.

Create hierarchy through proportion and placement. Keep small text readable
and secondary text clear enough for its task.

Match scale to context. Product screens need useful density. Editorial and
marketing surfaces can use larger contrasts in scale and more open space.

## Give color a role

Start with neutral surfaces and a clear text hierarchy. Add color for status,
selection, emphasis, data, or established brand meaning.

Define semantic tokens for page backgrounds, component backgrounds, borders,
primary text, secondary text, and interaction states.

Keep default, hover, active, focus, selected, and disabled states distinct.
Pair meaningful color with text, shape, or another perceivable cue.

Resolve colors by role in each theme. Check contrast on the actual surface,
including overlays and nested components.

## Make surfaces precise

Use space and alignment to group content. Add a border or surface when it
clarifies a boundary.

Draw shared borders once. Keep radius, fill, stroke, and shadow consistent
for surfaces with the same role.

Use the lowest elevation that clearly expresses the layer. Match visual
elevation to stacking order. Preserve visible focus and semantic roles.

Prefer flat resting surfaces. Use depth for raised content and overlays when
it helps explain their relationship to the page.

## Write useful interface text

Follow the product's capitalization convention.
Name actions clearly. Include the object when it resolves ambiguity.
Explain errors with the problem and the next useful action.
Give empty states a clear way forward.

## Preserve function during reduction

Keep labels, affordances, focus indicators, feedback, and recovery paths.
Remove repeated containers, competing accents, and effects that add no meaning.

Reuse existing components before creating variants. Confirm that documented
Geist packages, classes, or APIs exist in the project before using them.

For interaction contracts, motion, haptics, interruption, and recovery, use
[interface-design](../SKILL.md) when those decisions are in scope.

## Check the result

Check real content at narrow and wide widths, with large text and relevant
light and dark themes. Inspect keyboard focus and hover, pressed, selected,
disabled, pending, and error states where relevant.

The person should be able to identify the primary task, understand the groups,
read the content, and recognize the current state.

Report what was observed and what remains unverified. A static image supports
composition findings; runtime behavior needs runtime evidence.

## Sources

This skill adapts Swiss composition and Geist into a practical design method.
The combined method is a local interpretation.

Consult the relevant source when exact tokens, components, or APIs matter:

- [Swiss Grid — Poster House](https://swissgrid.posterhouse.org/)
- [Geist introduction](https://vercel.com/geist/introduction)
- [Typography](https://vercel.com/geist/typography)
- [Colors](https://vercel.com/geist/colors)
- [Materials](https://vercel.com/geist/materials)
- [Grid](https://vercel.com/geist/grid)

Additional workflow ideas were adapted from
[0xdenny218's Vercel Geist skill](https://github.com/0xdenny218/vercel-geist-design-skill/blob/main/skills/vercel-geist-design/SKILL.md).
Use official Geist documentation to resolve conflicting implementation guidance.
