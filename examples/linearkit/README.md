# LinearKit solve example

Solves a two-variable system with a pivot row exchange, then fits a straight line to three observations using least squares.

From the repository root, create an isolated consumer using the existing sealed
package (building directly in this checkout discovers unrelated app resources):

```sh
example_dir=$(mktemp -d)
mkdir "$example_dir/packages"
cp examples/linearkit/main.bui "$example_dir/main.bui"
cp packages/linearkit-0.1.0.buipkg "$example_dir/packages/"
(cd "$example_dir" && buoy main.bui --check --diagnostic-format json && buoy main.bui -o app && ./app)
```

For a standalone consumer, copy `main.bui` into a fresh directory and place
`linearkit-0.1.0.buipkg` from the repository's `packages/` in that directory's
`packages/`. Run `buoy main.bui -o app` and `./app` there. No native libraries
or services are required.

The solve succeeds with components 3 and 2 and zero scaled residual. The fit succeeds with intercept approximately 1.16667 and slope 0.5.

Maintainers run the private validation suite before release. See the repository README for public build instructions.
