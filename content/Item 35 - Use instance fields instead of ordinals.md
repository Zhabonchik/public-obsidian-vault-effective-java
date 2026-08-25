Why not use ordinal() method?
- If we rearrange the order of constants, it will break all the logic
- If we need to add a constant for number 3, but there is no for number 2, then we will have to introduce an unused dummy constant

The better approach is to create a final field (instance) and set its value in constructor.