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
* The `bool`-returning member functions of `never_stop_token` are made
  `[[nodiscard]]` for consistency with `[[stop_token]]`.
* The behavior of `in_place_stop_source::stop_possible()` is changed to
  reflect the fact that an `in_place_stop_source` always has "ownership" of
  a stop state (there is no `std::nostopstate_t` constructor). This is
  for consistency with `std::stop_source`.
