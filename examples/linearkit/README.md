# LinearKit solve example

Solves a two-variable system with a pivot row exchange, then fits a straight line. The solution is 3 and 2 with zero scaled residual; the fit has intercept about 1.16667 and slope 0.5.

From this repository root, with Buoy and BPM installed:

```sh
package_source="$PWD"
example_dir=$(mktemp -d)
cp examples/linearkit/main.bui "$example_dir/main.bui"
(cd "$example_dir" && bpm init && bpm add linearkit --path "$package_source" && bpm build main.bui -o app && ./app)
```

BPM builds from this checkout's package source and installs its declared
dependencies into the consumer project.
