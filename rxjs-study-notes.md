# Rxjs


## Operators

Operators return new observables (immutable) leaving the original (source) observables untouched.

`switchMap`
- switch to the inner/returned observable anytime the outer/source event arrives
- _cancels_ the previous subscription and starts a new one
- commonly used to "start" an observable based on UI change events - e.g. button click, input change