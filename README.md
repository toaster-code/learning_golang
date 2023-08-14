# learning_golang
Tips for using Go for beginners (notes and references)

# Using imports and packages
The use of packages in golang is different from python.
To split a project in .go files, one can put them in the same folder as the main program (usually the name of the project or main.go), or inside subfolders.

Relative imports are forbidden after Go 1.11, so this is the recippe:

Consider a project named "go_game_jumper" with this tree:

```cmd
go_game_jumper\
go_game_jumper\main.go
go_game_jumper\auxiliary.go
go_game_jumper\src\tiles\tiles.go
```

To import, one must name the packages as the name of the parent folder (recommended to ease the namespace thing, but not obligatory):

auxiliary.go:
```go
package main
...
```

main.go:
```go
package main
import (
	"fmt"	
	"log"
	"go_game_jumper/src/tiles"

var demo mytiles.Test = 10 // declared a var demo of type Test, which is equivalent to an integer
...
```

tiles.go:
```go
package mytiles

type Test int
...
```

TLDR: You should import subfolders based on the project main name. And the .go files defines the namespace (the namespace is the "y" in "import x as y" in python, for reference).
So to use the namespace in main one must see the package name declared in the subfolder "tiles" in the example above.

# namespaces

One thing to note is that only exported types and functions in a will be available externally. That is, types and functions whose names begin with a capital letter.

To simplify the usage of types from external packages by assigning them to a shorter alias.

```go
Copy code
package main

import (
	"fmt"
	"log"
	t "go_game_jumper/src/tiles" // Import the tiles package and assign an alias "t"
	"github.com/hajimehoshi/ebiten"
	"github.com/hajimehoshi/ebiten/ebitenutil"
)

// ...

// the player
var player t.Tile = t.Tile{ // Use the alias "t" here
	image:    nil,
	x:        50,
	y:        50,
	vx:       0,
	vy:       0,
	width:    16,
	height:   16,
	standing: true,
	blocking: true,
}
```
By assigning the alias "t" to the tiles package, you can use "t.Tile" to refer to the "Tile" type throughout your "main.go" file.
Use meaningful names to avoid confusion.





