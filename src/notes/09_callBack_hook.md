
#### Best Practices
- Use `useCallback` to memoize functions and prevent unnecessary re-creation:
  ```jsx
  const handleRemovePlace = useCallback(() => {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    setModalIsOpen(false);
    const storedIds = JSON.parse(localStorage.getItem("selectedPlaces")) || [];
    localStorage.setItem(
      "selectedPlaces",
      JSON.stringify(storedIds.filter((id) => id !== selectedPlace.current))
    );
  }, [selectedPlace]);
  ```

By memoizing `handleRemovePlace`, you ensure that `onConfirm` remains stable across renders, avoiding unnecessary effect re-executions.