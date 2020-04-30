<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <span class="headline">Todoリスト</span>
      </div>
    </v-app-bar>

    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <span>タスク数: {{ getLength }}</span>
            <v-text-field
              label="タスクを入力してください"
              v-model="state.todo"
            ></v-text-field>
            <v-btn @click="add">追加</v-btn>
            <v-list>
              <v-list-item
                v-for="(todo, index) in state.todos"
                :key="index"
              >
                <v-list-item-content>
                  <v-list-item-title v-text="todo" />
                </v-list-item-content>
                <v-list-item-icon>
                  <v-icon @click="remove(index)">mdi-delete</v-icon>
                </v-list-item-icon>
              </v-list-item>
            </v-list>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import { reactive, computed } from '@vue/composition-api'

export default {
  name: 'App',

  setup () {
    const state = reactive({
      todo: '',
      todos: []
    })

    const getLength = computed(() => state.todos.length)

    const add = () => {
      state.todos.push(state.todo)
      state.todo = ''
    }

    const remove = index => state.todos.splice(index, 1)

    return {
      state,
      getLength,
      add,
      remove
    }
  }
}
</script>
