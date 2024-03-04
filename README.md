### Task
Language C++. C++ version - by your choice. Create a class `CoinsForest<I, G>` - a variant of the key-value data structure. `I` stands for the key type (interpreted as ID), and `C` represents the value (interpreted as Coins). You must create also tests to cover all class functionality. The class should implement the following methods:

1. `get(I id)`:
    If `id` does not exists or is __consumed__, then returns an error, otherwise returns the amount of coins corresponding to the given `id`.

2. `new_root(I id, C coins)`:
    Adds a new key-value pair (`id`, `coins`). Returns `void` in case of success or an error if the `id` already exists.

3. `make_child_from(I parent_id, I child_id, C coins)`:
    Adds a new key-value pair (`child_id`, `coins`). Also, subtracts `coins` from the `parent_id`'s value. `parent_id` becomes the parent for `child_id`, and `child_id` becomes a direct descendant of `parent_id`. In case of success returns `void`. In case of an error should return an error variant:

    - `parent_id` does not exist or is __consumed__
    - `child_id` already exists
    - insufficient coins at `parent_id`.

4. `consume(I id)`:
    __Consumes__ the given key-value pair. If `id` does not exists or is already __consumed__, then returns an error. Otherwise after this method execution must be guarantied:

    - If `id` has at least one __not-consumed__ descendant, then `id` is not deleted but marked as __consumed__.
    - If `id` has no descendants, then `id` is deleted, as well as all its __consumed__ ancestors having no __not-consumed__ descendants.
    - If `id` has a __not-consumed__ ancestor, its coins are transferred to the nearest __not-consumed__ ancestor, and 0 is returned. Otherwise, the amount of `id` coins is returned as the result from the function.

5. `sub_coins(I id, C coins)`:
    Subtracts `coins` from the value for `id`. Returns `void` in case of success. Returns an error variant otherwise:

    - `id` does not exist or is __consumed__
    - insufficient coins at `id`.

### Tips:

1. __Consumed__ - is property which identifies, that some `id` is not deleted, but cannot be used in any `CoinsForest` methods. __consumed__ `id` exists in the `CoinsForest` only if it has some __not-consumed__ descendants.
2. In C++ 23, you can use [std::expected](https://en.cppreference.com/w/cpp/utility/expected) as results for methods.
3. You can use [std::map](https://en.cppreference.com/w/cpp/container/map) for internal representation.
4. Instead of using pointers to child/parent you can use `id` - it's not performance efficient, but can simplify work for you.
