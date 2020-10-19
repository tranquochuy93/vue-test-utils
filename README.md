# vue-test-utils

#### wait for vuejs rendering
- use flush-promises
  - yarn add flush-promises
  - import flushPromises from 'flush-promises';
  - async () => {}
  - sync: false
  - await flushPromises();
  ```js
  ...
  import flushPromises from 'flush-promises';

  describe('...', () => {
    ...
    test('...', async () => {
      const wrapper = mount(..., {
          ...
          sync: false
      });
      ...
      button.trigger('click');
      await flushPromises();

      expect(....
    }
  }
  ```
