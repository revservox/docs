# Auto-Range



### How to activate a position

To setup a position it needs to be approved for the Auto-Exit contract with `setApprovalForAll` and the method `configToken()` must be called.

`setApprovalForAll` is mandatory here because it is the only way that the newly created positions are approved automatically.

### How to remove a position

Call the `configToken()` function with all values set to default.



##
