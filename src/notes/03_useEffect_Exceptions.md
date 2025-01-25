# Overusing `useEffect()`: React Best Practices

## Side Effects in React

### What is a Side Effect?
- Operations unrelated to direct component rendering
- Tasks that don't immediately impact the current render cycle
- Examples include:
  - Fetching user location
  - Saving data to local storage
  - Browser API interactions

## When to Avoid `useEffect()`
- Not every side effect requires `useEffect()`
- `useEffect()` introduces an extra render cycle
- Use only when absolutely necessary

## Local Storage Example

### Scenario: Saving Selected Places
```jsx
function handleSelectPlace(id) {
  // State update (rendering-related)
  setPickedPlaces((prevPickedPlaces) => {
    if (prevPickedPlaces.some((place) => place.id === id)) {
      return prevPickedPlaces;
    }
    const place = AVAILABLE_PLACES.find((place) => place.id === id);
    return [place, ...prevPickedPlaces];
  });

  // Side effect: Local storage interaction
  const storedIds = JSON.parse(localStorage.getItem("selectedPlaces")) || [];
  if (storedIds.indexOf(id) === -1) {
    localStorage.setItem("selectedPlaces", JSON.stringify([id, ...storedIds]));
  }
}
```

### Using `localStorage`
- Browser-provided memory storage
- `.setItem()` saves data persistently
- Data must be converted to string
- Example: `localStorage.setItem("selectedPlaces", JSON.stringify([]))`

### Breaking Down the Side Effect
- State update: Top part of the function
- Local storage interaction: Side effect
- Not inherently bad, just unrelated to rendering

## Why Not Use `useEffect()` Here?
- Function runs only on user interaction
- Not on every re-render
- Hooks can only be used at the root level of a function
- No risk of infinite loop

## Key Considerations
- Side effects aren't always problematic
- Choose the right approach based on specific use case
- Prioritize clean, readable code
- Minimize unnecessary render cycles

### Best Practices
- Use `useEffect()` sparingly
- Consider alternative patterns
- Keep rendering logic separate from side effects
- Optimize component performance

## Important Reminder
Not every side effect requires `useEffect()`. 
Choose the most appropriate and efficient method for your specific scenario.