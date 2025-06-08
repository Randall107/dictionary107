<template>
  <div class="container mt-5">
    <ul class="nav nav-tabs mb-3">
      <li class="nav-item" v-for="tab in tabs" :key="tab.id">
        <button
          class="nav-link"
          :class="{ active: activeTab === tab.id }"
          @click="activeTab = tab.id"
        >
          {{ tab.name }}
        </button>
      </li>
    </ul>

    <div class="tab-content p-3 border border-top-0">
      <div
        v-for="tab in tabs"
        :key="tab.id"
        v-show="activeTab === tab.id"
        class="tab-pane active"
      >
        <form @submit.prevent="handleSubmit(tab.id)">
          <div
            v-for="(field, index) in tab.fields"
            :key="index"
            class="mb-3"
          >
            <label :for="tab.id + '-' + (field.key || 'default')" class="form-label">
              {{ field.label }}
            </label>
            <input
              type="text"
              class="form-control"
              :id="tab.id + '-' + (field.key || 'default')"
              v-model="formData[tab.id][field.key || 'default']"
              :placeholder="field.placeholder"
            />
          </div>

          <button type="submit" class="btn" :class="tab.buttonClass">
            {{ tab.buttonText }}
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "VocabApp",
  data() {
    return {
      activeTab: "read",
      tabs: [
        {
          id: "read",
          name: "Read",
          fields: [
            { label: "Look up" }
          ],
          buttonClass: "btn-primary",
          buttonText: "Submit"
        },
        {
          id: "delete",
          name: "Delete",
          fields: [
            { label: "Delete" }
          ],
          buttonClass: "btn-primary",
          buttonText: "Submit"
        },
        {
          id: "update",
          name: "Update",
          fields: [
            { key: "en", label: "Enlish" },
            { key: "th", label: "Thai" }
          ],
          buttonClass: "btn-primary",
          buttonText: "Submit"
        },
        {
          id: "post",
          name: "Post",
          fields: [
            { key: "en", label: "Enlish" },
            { key: "th", label: "Thai" }
          ],
          buttonClass: "btn-primary",
          buttonText: "Submit"
        }
      ],
      formData: {
        read: { default: "" },
        delete: { default: "" },
        update: { oldWord: "", newDef: "" },
        post: { word: "", definition: "" }
      }
    };
  },
  methods: {
    handleSubmit(tabId) {
      const data = this.formData[tabId];
      console.log(`Form submitted for ${tabId}:`, data);
      alert(`Submitted for ${tabId.toUpperCase()}:\n${JSON.stringify(data, null, 2)}`);
    }
  }
};
</script>

<style>
body {
  background-color: #f8f9fa;
}
</style>
