<template>
  <div class="feature-item column is-half">
    <i :class="['feature-item__icon', iconName]"
       aria-hidden="true"/>
    <h4 class="feature-item__title">
      {{ title }}
    </h4>
    <p class="feature-item__text">
      {{ text }}
    </p>
  </div>
</template>

<script>
export default {
    name: 'FeatureItem',
    props: {
        iconName: {
            type: String,
            default: '',
        },
        title: {
            type: String,
            default: '',
        },
        text: {
            type: String,
            default: '',
        },
    },
}
</script>

<style lang="scss" scoped>
    .feature-item {

        &__icon {
            font-size: 48px;
            float: left;
            color: #007BFF;
        }

        &__title {
            font-size: 20px;
            font-weight: 700;
            margin: 5px 0 10px 60px;
            color: #2D2926;
            font-family: "Raleway", sans-serif;
            line-height: 1.5;
        }

        &__text {
            font-size: 15px;
            color: #2d2926e3;
            margin-left: 60px;
            margin-top: 0;
            margin-bottom: 1rem;
        }
    }
</style>
