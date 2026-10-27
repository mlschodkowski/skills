# Fusion iteration

This preserves the user's current Allegro issue convention. Explicit task or
repository instructions override it.

Project: `Fusion`, number `383`, owner `allegro-internal`.

1. Add the created issue with `gh project item-add 383 --owner allegro-internal
   --url <issue-url> --format json`, or the connector equivalent. Keep its item ID.
2. Read the project ID and iteration field through GraphQL. The field is a
   `ProjectV2IterationField`; read `configuration.iterations` with `id`, `title`,
   `startDate`, and `duration`.
3. Use today's date in Europe/Warsaw. Select the iteration where
   `startDate <= today < startDate + duration` in days.
4. Set it with `gh project item-edit --id <item-id> --project-id <project-id>
   --field-id <field-id> --iteration-id <iteration-id>`, or the connector equivalent.

If the project cannot be found, ask which project to use. If project access is
missing, report it; for `gh`, the user can run `gh auth refresh -s project`.
If there is no iteration field or current iteration, leave the issue on the
project, skip iteration assignment, and say so. Report partial success exactly.
