<template>
  <div class="content__diameter">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите размер</h2>
      <div class="sheet__content diameter">
        <AppRadioButton
          v-for="item in sizes"
          :key="item.id"
          :item="item"
          :classes="`diameter__input diameter__input--${item.value}`"
          @onRadioChange="$emit('onRadioChange', $event)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AppRadioButton from "@/common/components/RadioButton";
import { mapGetters } from "vuex";
import { gettersTypes } from "@/store/modules/builder";

export default {
  name: "AppBuilderSizeSelector",
  components: { AppRadioButton },
  computed: {
    ...mapGetters({
      sizes: gettersTypes.sizes,
    }),
  },
};
</script>
