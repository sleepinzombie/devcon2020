<template>
  <div class="sponsor-level-wrapper"
       :class="tierClass">
    <h4 class="tier-title">{{tier}}</h4>

    <section class="sponsors-wrapper"
             :class="getWrapperSize">
      <SponsorItem v-for="(sponsor, index) of sponsors"
                   :key="index"
                   :sponsor="sponsor" />
    </section>
  </div>
</template>

<script>
import SponsorItem from "@/components/sponsor-item.vue";

export default {
  name: "SponsorList",

  props: {
    sponsors: {
      type: Array,

      required: true,

      validator(value) {
        const isValidArray = value.length;
        return isValidArray;
      }
    },

    tier: {
      type: String,

      required: true,

      validator(value) {
        return !!value;
      }
    }
  },

  components: {
    SponsorItem
  },

  computed: {
    tierClass() {
      const formatted = this.tier.split(" ").join("-");
      return formatted.toLowerCase();
    },

    getWrapperSize() {
      const MEDIUM_TIERS = ["Speaker Sponsor", "Speaker", "Silver"];
      const SMALL_TIERS = [
        "Happy Hour Partner",
        "Silver",
        "Bronze",
        "Internet",
        "Media Partner",
        "Day Care"
      ];

      const medium = MEDIUM_TIERS.find(item => item === this.tier);
      const small = SMALL_TIERS.find(item => item === this.tier);

      let className = "";

      if (medium) {
        className = "medium";
      }

      if (small) {
        className = "small";
      }

      className = className ? `${className}-wrapper` : "";

      return className;
    }
  }
};
</script>

<style lang="scss">
.sponsor-level-wrapper {
  // *styling to be defined
}

.tier-title {
  // *styling to be defined
}

.sponsors-wrapper {
  display: flex;
  flex-wrap: wrap;
  padding: 10px 0 30px;
  justify-content: center;
  align-items: center;
  &:last-child {
    // border-bottom: 1px solid rgba(#fff, 0.3);
  }
}

.medium-wrapper {
  .sponsor-logo {
    img {
      width: 190px;
    }
  }
  // @media screen and (max-width: $tablet) {
  @media screen and (max-width: 768px) {
    .sponsor-logo {
      &:nth-child(even) {
        padding: 5px;
      }
      img {
        width: 150px;
      }
    }
  }
}
.small-wrapper {
  .sponsor-logo {
    img {
      width: 150px;
    }
  }
  // @media screen and (max-width: $tablet) {
  @media screen and (max-width: 768px) {
    .sponsor-logo {
      &:nth-child(even) {
        padding: 5px;
      }
      img {
        width: 100px;
      }
    }
  }
}
</style>