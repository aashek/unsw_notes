Most info recieved from https://lukakerr.github.io/uni/3161-notes#abstract-data-types

### Bag ADT Example

-   Specified by three operations
    -   `emptyBag` - BB
    -   `addToBag` - (B→Int→B)(B→Int→B)
    -   `average` - (B×Int)(B×Int)

in this case we think, it cannot be forall, since its impossible
so we write the type as a product of all possible types from the functions.


-   The type for this ADT is ∃B.B×(B→Int→B)×(B→Int)∃B.B×(B→Int→B)×(B→Int)