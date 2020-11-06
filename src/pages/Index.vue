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
          class="q-gutter-md"
          >
          <div class="row items-start justify-between">
            <q-input
              class="col q-field--with-bottom"
              outlined
              v-model="email"
              type="email"
              label="Эл. почта"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Обязательно для заполнения']"
            />
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>введите свою почту</q-tooltip>
            </q-icon>
          </div>
          <q-separator />
          <div class="row items-start justify-between">
            <q-input
              class="col q-field--with-bottom"
              outlined
              v-model="name"
              type="text"
              label="Имя"
            />
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>как вас зовут?</q-tooltip>
            </q-icon>
            <q-separator />
          </div>
          <div class="row items-start justify-between">
            <q-input
              class="col q-field--with-bottom"
              outlined
              v-model="coordinates"
              label="Координаты"
            >
            <template v-slot:append>
              <q-btn
                round
                flat
                icon="my_location"
                @click="showMap = true" />
            </template>
            </q-input>
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>где находится дерево?</q-tooltip>
            </q-icon>
          </div>
          <q-separator />
          <div class="row items-start justify-between">
            <q-select
              class="col q-field--with-bottom"
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
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>что это за дерево? может быть клён?</q-tooltip>
            </q-icon>
          </div>
          <div class="q-mr-xl">
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
          <q-separator />
          <div class="row items-start justify-between">
            <q-select
              class="col"
              outlined
              label="Состояние дерева"
              v-model="species"
              :options="treeSpecies"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Обязательно для заполнения']">
            </q-select>
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>как оно выглядит?</q-tooltip>
            </q-icon>
          </div>
          <q-separator />
          <section class="q-mb-lg">
            <div class="row items-start justify-between">
              <q-input
                class="col q-pb-lg"
                outlined
                label="Толщина ствола на высоте груди (~1.3м), см"
                v-model="thick"
                step="0.1"
                type="number"
              />
              <q-icon
              class="q-ml-sm"
                name="help_outline"
                color="grey"
                size="md"
              >
              <q-tooltip>широкое?</q-tooltip>
              </q-icon>
            </div>
            <q-btn-toggle
              class="q-mr-xl custom-btns"
              v-model="thickness"
              spread
              no-caps
              rounded
              unelevated
              toggle-color="primary"
              color="white"
              text-color="primary"
              :options="[
                {label: 'В обхват', value: 'around'},
                {label: 'Диаметр', value: 'diameter'}
              ]"
            />
          </section>
          <q-separator />
          <div class="row items-start justify-between">
            <q-input
            class="col"
              outlined
              label="Высота дерева, м"
              v-model="height"
              type="number"
            />
            <q-icon
            class="q-ml-sm"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>высоченное наверное?</q-tooltip>
            </q-icon>
          </div>
          <q-separator/>
          <div class="row items-start justify-between">
            <section class="col q-pb-lg">
              <p class="q-pb-xs">Освещённость солнцем</p>
              <q-btn-toggle
                class="custom-btns"
                v-model="illumination"
                spread
                no-caps
                rounded
                unelevated
                toggle-color="primary"
                color="white"
                text-color="primary"
                :options="[
                  {label: 'Полностью', value: 'full'},
                  {label: 'Частично', value: 'partly'},
                  {label: 'В тени', value: 'shadow'}
                ]"
              />
            </section>
            <q-icon
              class="q-ml-sm align-self"
              name="help_outline"
              color="grey"
              size="md"
            >
            <q-tooltip>очоки нннада?</q-tooltip>
            </q-icon>
          </div>
          <div>
            <q-btn
            class="q-btn q-btn-item non-selectable no-outline full-width q-btn--unelevated q-btn--rectangle q-btn--rounded bg-positive q-btn--actionable q-focusable q-hoverable q-btn--no-uppercase"
            label="Добавить дерево и рассчитать параметры"
            type="submit"
            color="primary"/>
          </div>
          </q-form>
        </div>
      <q-dialog v-model="showMap">
      <q-card>
        <q-card-section class="row items-center q-pb-none">
          <q-btn icon="close" flat round dense v-close-popup />
          <yandex-map :settings="settings" :coords="coordinates">
            <ymap-marker
            marker-id="123"
            :coords="coords"
            :icon="markerIcon"/>
          </yandex-map>
        </q-card-section>
        <q-btn flat type="button" label="Выбрать" v-close-popup/>
      </q-card>
      </q-dialog>
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
.align-self {
  align-self: center;
}
</style>

<script>
const stringOptions = [
  {
    label: 'Берёза (birch spp)',
    latinLabel: 'Betula'
  },
  {
    label: 'Берёза пушистая (Downy birch)',
    latinLabel: 'Betula pubescens'
  },
  {
    label: 'Берёза бородавчатая (повислая) (European white birch)',
    latinLabel: 'Betula pendula'
  },
  {
    label: 'Боярышник обыкновенный(Smooth hawthorm)',
    latinLabel: 'Crataegus laevigata'
  },
  {
    label: 'Бук крупнолистный(American beech)',
    latinLabel: 'Fagus grandifolia'
  }
]

const treeOptions = [
  'Сухостой',
  'Усыхающие',
  'Сильно ослабленное',
  'Ослабленное',
  'Без признаков ослабления',
  'Выберите состояние'
]

const settings = {
  apiKey: 'c7da0612-efe8-4c2b-b871-4a6cbfcd6d9c',
  lang: 'ru_RU',
  coordorder: 'latlong',
  version: '2.1'
}

import { yandexMap } from 'vue-yandex-maps'

export default {
  name: 'PageIndex',
  data () {
    return {
      email: null,
      name: null,
      text: null,

      model: null,

      treeType: 'regular',
      options: stringOptions,
      species: null,
      treeSpecies: treeOptions,
      thick: 10,
      thickness: 'around',
      illumination: 'full',
      height: null,
      coordinates: '51.73103966, 36.19461017',
      showMap: false,
      settings: settings,
      markerIcon: {
        layout: 'default#imageWithContent',
        imageHref: 'https://image.flaticon.com/icons/png/512/33/33447.png',
        imageSize: [43, 43],
        imageOffset: [0, 0],
        content: '123 v12',
        contentOffset: [0, 15],
        contentLayout: '<div style="background: red; width: 50px; color: #FFFFFF; font-weight: bold;">$[properties.iconContent]</div>'
      }
    }
  },
  components: { yandexMap },
  methods: {
    onSubmit () {
      if (this.data == null) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning'
        })
      }
    },
    onReset () {
      this.email = null
      this.name = null
      this.text = null
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
  },
  computed: {
  }
}
</script>
