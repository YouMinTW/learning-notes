## Object comparison for dirty field from React-hook-form

```js
function getDirtyFields(dirtyFields, formValues) {
  if (typeof dirtyFields !== 'object' || dirtyFields === null || !formValues) {
    return {};
  }

  return Object.keys(dirtyFields).reduce((accumulator, key) => {
    const isDirty = dirtyFields[key];
    const value = formValues[key];

    // If it's an array, apply the logic recursively to each item
    if (Array.isArray(isDirty)) {
      // eslint-disable-next-line no-underscore-dangle
      const _dirtyFields = isDirty.map((item, index) => getDirtyFields(item, value[index]));
      if (_dirtyFields.length > 0) {
        // eslint-disable-next-line no-param-reassign
        accumulator[key] = _dirtyFields;
      }
    }
    // If it's an object, apply the logic recursively
    else if (typeof isDirty === 'object' && isDirty !== null) {
      // eslint-disable-next-line no-param-reassign
      accumulator[key] = getDirtyFields(isDirty, value);
    }
    // If it's a dirty field, get the value from formValues
    else if (isDirty) {
      // eslint-disable-next-line no-param-reassign
      accumulator[key] = value;
    }

    return accumulator;
  }, {});
}

describe('getDirtyFields', () => {
  it('should return an empty object if dirtyFields is not an object or is null', () => {
    expect(getDirtyFields(null, {})).toEqual({});
    expect(getDirtyFields('not an object', {})).toEqual({});
  });

  it('should return an empty object if formValues is not provided', () => {
    expect(getDirtyFields({}, null)).toEqual({});
  });

  it('should return an object with dirty fields', () => {
    const dirtyFields = { field1: true, field2: false, field3: true };
    const formValues = { field1: 'value1', field2: 'value2', field3: 'value3' };
    expect(getDirtyFields(dirtyFields, formValues)).toEqual({ field1: 'value1', field3: 'value3' });
  });

  it('should handle nested objects', () => {
    const dirtyFields = { field1: { subfield1: true, subfield2: false }, field2: true };
    const formValues = { field1: { subfield1: 'value1', subfield2: 'value2' }, field2: 'value3' };
    expect(getDirtyFields(dirtyFields, formValues)).toEqual({ field1: { subfield1: 'value1' }, field2: 'value3' });
  });
});
```
