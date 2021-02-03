<template lang="pug">
v-card(elevation=18, width="700" shaped )
  v-card-title.justify-center {{ $t('card.title') }}
  v-card-text
    v-form(ref="form")
      v-text-field(
        prepend-icon="fas fa-address-book",
        autocomplete,
        clearable,
        :rules="[emptyRules, phoneRules]",
        rounded,
        counter="10",
        filled,
        flat,
        :hint="$t('card.form.phone.hint')",
        validate-on-blur,
        @click:prepend="selectContant",
        v-model="phone"
      )
        template(slot="label")
          small.warning--text *
          template {{ $t('card.form.phone.label') }}
      v-textarea(
        :label="$t('card.form.message.label')",
        prepend-icon="far fa-comment-alt",
        counter="255",
        clearable,
        rounded,
        filled,
        flat,
        rows="1",
        auto-grow,
        :hint="$t('card.form.message.label')",
        v-model="text"
      ) 
    v-divider.my-5(color="primary" )
  v-card-actions.mx-2
    template(v-for="(item, index) in items")
      v-btn(
        :key="item.key",
        :color="item.color",
        x-large,
        icon,
        @click="sendMessege(item.icon)"
      ) 
        v-icon {{ `fab fa-${item.icon}` }}
      v-spacer(v-if="index < items.length - 1")
</template>
<script>
export default {
  data: () => ({
    phone: null,
    text: null,
    items: [
      { icon: "viber", color: "#665CAC" },
      { icon: "whatsapp", color: "#4fce5d" },
      { icon: "skype", color: "#00aff0" },
      { icon: "telegram", color: "#0088cc" },
      { icon: "weixin", color: "#7BB32E" },
    ],
  }),
  methods: {
    phoneRules(v) {
      return (
        /^05\d([-]{0,1})\d{7}$/.test(v) || this.$t("card.form.rules.phone")
      );
    },
    emptyRules(v) {
      return !!v || "שדה חובה";
    },
    maxCharters(v) {
      (v && v.length <= 255) || "מקסימום 255 תווים";
    },
    selectContant() {
      const supported = "contacts" in navigator && "ContactsManager" in window;
      if (supported) {
      } else alert("dont working");
    },
    sendMessege(type) {
      let link;
      switch (type) {
        case "viber":
          link = `viber://contact?number=%2B${this.phone}`;
          break;
        case "whatsapp":
          link = `https://wa.me/${this.phone}?text=${this.text}`;
        case "skype":
          link = `skype:echo${this.phone}?chat`;
          break;
        case "telegram":
          link = `https://telegram.me/share/url?url=<URL>&text=<TEXT>`;
          break;
      }
      window.open(link)
    },
  },
};
</script>