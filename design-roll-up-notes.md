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
* Sender queries are moved into a separate queryable "attributes" object
  that is accessed by passing the sender to `get_attrs()`. The `sender`
  concept is reexpressed to require `get_attrs()` and separated from
  a new `sender_in<Snd, Env>` concept for checking whether a type is
  a sender within a particular execution environment.
* The placeholder types `no_env` and `dependent_completion_signatures<>`
  are no longer needed and are dropped.
* `ensure_started` and `split` are changed to persist the result of
  calling `get_attrs()` on the input sender.