<template>
  <Page class="page">
    <ActionBar title="My Tasks" class="action-bar" />

    <TabView height="100%" androidTabsPosition="bottom">
      <TabViewItem title="To Do">
        <StackLayout orientation="vertical" width="100%" height="100%">
          <GridLayout columns="2*, *" rows="*" width="100%" height="25%">
            <TextField
              col="0"
              row="0"
              hint="Type new task..."
              editable="true"
              @returnPress="onButtonTap"
              v-model="textFieldValue"
            />

            <Button col="1" row="0" text="Button" @tap="onButtonTap" />
          </GridLayout>

          <ListView for="todo in todos" @itemTap="onItemTap" style="height:75%">
            <v-template>
              <Label :text="todo.name" class="list-group-item-heading" textWrap="true" />
            </v-template>
          </ListView>
        </StackLayout>
      </TabViewItem>

      <TabViewItem title="Completed">
        <Label text="This tab will list completed tasks for tracking." textWrap="true" />
      </TabViewItem>
    </TabView>
  </Page>
</template>

<script lang="ts">
export default {
  data() {
    return {
      msg: "Hello World!",
      todos: [],
      textFieldValue: ""
    };
  },

  methods: {
    onItemTap: function(args) {
      console.log("Item with index: " + args.index + " tapped");
    },

    onButtonTap() {
      if (this.textFieldValue === "") return; // Prevents users from entering an empty string.
      console.log("New task added: " + this.textFieldValue + "."); // Logs the newly added task in the console for debugging.
      this.todos.unshift({ name: this.textFieldValue }); // Adds tasks in the ToDo array. Newly added tasks are immediately shown on the screen.
      this.textFieldValue = ""; // Clears the text field so that users can start adding new tasks immediately.
    }
  }
};
</script>

<style scoped>
.home-panel {
  vertical-align: center;
  font-size: 20;
  margin: 15;
}

.description-label {
  margin-bottom: 15;
}
</style>