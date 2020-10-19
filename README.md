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
- await Vue.nextTick() / await wrapper.vm.$nextTick();
 - import Vue from 'vue';
 - await Vue.nextTick();
 
 #### trigger event
 - vuetify
   ```js
   const button = wrapper.findComponent({ name: 'v-btn' });
   button.vm.$emit('click');
   ```
 #### mock store, action, getter
 - import { mount, createLocalVue } from '@vue/test-utils';
 - const localVue = createLocalVue();
 ```js
 import { mount, createLocalVue } from '@vue/test-utils';
 import Vuetify from 'vuetify';
 import Vuex from 'vuex';
 import Vue from 'vue';
 ...
 
 const localVue = createLocalVue();
 localVue.use(Vuex);
 
 describe('...', () => {
  let vuetify;
  let store;
  let actions;
  let getters;
  
  beforeEach(() => {
    vuetify = new Vuetify({});

    actions = {
      'test/index': jest.fn((item) => {
        return Promise.resolve({});
      }),
    };
    
    getters = {
      'test/getDataList': () => ({
        data: []
      }),
    };

    store = new Vuex.Store({
      state: {},
      actions,
      getters,
    });
  });
  
  test('...', async () => {
   const wrapper = mount(..., {
      localVue,
      store,
      vuetify,
      data: function() {
        return {}
      },
      template: `
        <div data-app>
          <... />
        </div>
      `,
      sync: false
  });
  await flushPromises();
  expect(actions['test/index']).toHaveBeenCalled();
 ```
