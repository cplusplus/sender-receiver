Design changes tweaks by LWG after the Kona meeting
===================================================

* `stoppable_token::stop_possible()` and `stoppable_token::stop_requested()`
  are now required to return precisely `bool`, not _`boolean-testable`_.
* The syntactic requirements for the `stoppable_token` have been relaxed such
  that an implementation is not required to check for callback constructibility
  from all permutations of `const` and `&`. The `const&` one is required
  and the rest become semantic constraints.
* We added a type alias `stop_callback_for_t` such that `stop_callback_for_t<T, CB>`
  is an alias for `typename T::template callback_type<CB>`.