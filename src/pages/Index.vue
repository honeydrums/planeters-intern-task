<template>
  <q-page class="q-pa-md">
    <div class="container">
      <h3 class="text-h3 text-center q-mt-none q-mb-md">Добавить дерево</h3>
      <p class="text-black text-center q-mt-none q-mb-md">Заполните форму, чтобы определить выгоду от него.</p>
      <div class="q-pa-md">
      <div class="q-gutter-md">
        <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-gutter-md">
          <q-input
            class="q-field--with-bottom"
            outlined
            v-model="email"
            type="email"
            label="Эл. почта"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Обязательно для заполнения']"
          />
          <q-separator />
          <q-input
            class="q-field--with-bottom"
            outlined
            v-model="name"
            type="text"
            label="Имя"
          />
          <q-separator />
          <q-input
            class="q-field--with-bottom"
            outlined
            v-model="text"
            label="Координаты"
          />
          <q-separator />
          <q-select
            class="q-field--with-bottom"
            outlined
            label="Порода дерева"
            use-input
            hide-selected
            fill-input
            input-debounce="0"
            :value="model"
            :options="options"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Обязательно для заполнения']"
            @filter="filterFn"
            @input-value="setModel"
            hint="Введите 2 символа для подсказки" >
            <template v-slot:no-option>
              <q-item>
                <q-item-section class="text-grey">
                  Ничего не найдено
                </q-item-section>
              </q-item>
            </template>
          </q-select>
          <div>
            <q-btn-toggle
              class="custom-btns"
              v-model="treeType"
              spread
              no-caps
              rounded
              unelevated
              toggle-color="primary"
              color="white"
              text-color="primary"
              :options="[
                {label: 'Обычное', value: 'regular'},
                {label: 'Научное', value: 'science'}
              ]"
            />
          </div>
          <q-select
            outlined
            label="Состояние дерева"
            v-model="species"
            :options="treeSpecies"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Обязательно для заполнения']">
          </q-select>
          <q-input
            outlined
            label="Толщина ствола на выосте груди (~1.3м), см"
            v-model.number="thick"
            type="number"
          />
          <div>
            <q-btn class="q-btn q-btn-item non-selectable no-outline full-width q-btn--unelevated q-btn--rectangle q-btn--rounded bg-positive q-btn--actionable q-focusable q-hoverable q-btn--no-uppercase" label="Добавить дерево и рассчитать параметры" type="submit" color="primary"/>
          </div>
        </q-form>
      </div>
    </div>
  </div>
  </q-page>
</template>

<style lang="stylus">
.container {
  margin: 0 auto;
  max-width: 480px;
}
.custom-btns {
  border: 1px solid #5bd397;
}
</style>

<script>
const stringOptions = [
  'Берёза (birch spp)',
  'Берёза пушистая (Downy birch)',
  'Берёза бородавчатая (повислая) (European white birch)',
  'Боярышник обыкновенный(Smooth hawthorm)',
  'Бук крупнолистный(American beech)'
]

export default {
  name: 'PageIndex',
  data () {
    return {
      email: null,
      name: null,
      text: null,

      accept: false,

      model: null,

      treeType: 'regular',
      options: stringOptions,
      species: null,
      treeSpecies: [
        'Сухостой',
        'Усыхающие',
        'Сильно ослабленное',
        'Ослабленное',
        'Без признаков ослабления',
        'Выберите состояние'
      ],
      thick: 10
    }
  },
  methods: {
    onSubmit () {
      if (this.accept !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'Обязательно для заполнения'
        })
      }
    },
    onReset () {
      this.email = null
      this.name = null
      this.text = null
      this.accept = false
    },
    filterFn (val, update) {
      if (val === '') {
        update(() => {
          this.options = stringOptions
        })
        return
      }
      update(() => {
        const needle = val.toLowerCase()
        this.options = stringOptions.filter(v => v.toLowerCase().indexOf(needle) > -1)
      })
    },
    setModel (val) {
      this.model = val
    }
  }
}
</script>
