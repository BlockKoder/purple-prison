<template>
    <div class="footer">
        <div class="footer__store container">
            <div class="footer__copyright">
                <img src="/nav-logo.png" alt="PurplePrison" />
                <p>
                    © {{ new Date().getFullYear() }} PurplePrison. All rights
                    reserved.
                </p>
            </div>
            <div class="footer__links">
                <Button
                    v-if="appConfig.discordUrl"
                    tag="a"
                    :href="appConfig.discordUrl"
                    variant="secondary"
                    prepend-icon="discord"
                >
                    Join our Discord
                </Button>
            </div>
        </div>

        <div class="footer__tebex">
            <div class="footer__tebex-inner container">
                <div class="footer__tebex-description">
                    <a
                        :href="`https://www.tebex.io/?utm_source=store&utm_campaign=${appConfig.storeId}`"
                    >
                        <Icon
                            name="tebex"
                            width="51px"
                            :font-controlled="false"
                        />
                    </a>
                    <p>
                        {{ $t("footer.tebex.description") }}
                    </p>
                </div>

                <div class="footer__tebex__links">
                    <a href="https://checkout.tebex.io/impressum">
                        {{ $t("footer.tebex.impressum") }}
                    </a>
                    <a href="https://checkout.tebex.io/terms">
                        {{ $t("footer.tebex.tos") }}
                    </a>
                    <a href="https://checkout.tebex.io/privacy">
                        {{ $t("footer.tebex.privacy_policy") }}
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
const appConfig = useAppConfig();
</script>

<style lang="scss" scoped>
@use "~/assets/styles/settings" as *;
@use "~/assets/styles/tools";

.footer {
    width: 100%;
    margin-top: 50px;
    background: rgba(28, 27, 28, 0.94);
    border-top: 1px solid rgba(255, 255, 255, 0.08);

    &__store {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-items: center;
        margin: 0 auto;
        width: 100%;
        justify-content: space-between;
        padding: 16px 20px;
        gap: 15px;

        @include tools.media-breakpoint-up("md") {
            height: $footer-height;
            padding: 0 38px;
        }
    }

    &__tebex {
        display: flex;
        align-items: center;
        font-family: $font-family;
        min-height: $footer-tebex-height;
        background-color: $footer-tebex-bg;
        color: $footer-tebex-color;
        font-size: $footer-tebex-font-size;
        border-top: 1px solid rgba(143, 162, 194, 0.24);

        &-inner {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            align-items: center;
            height: 100%;
            gap: 20px;
            width: 100%;
            margin: 0 auto;
            padding: 16px 20px;

            @include tools.media-breakpoint-up("md") {
                padding: 0 38px;
            }
        }

        &-description {
            svg {
                min-width: 51px;
            }

            display: flex;
            align-items: center;
            gap: 20px;

            p {
                @include tools.media-breakpoint-up("md") {
                    max-width: 450px;
                }

                @include tools.media-breakpoint-up("lg") {
                    max-width: initial;
                }
            }
        }

        p {
            margin-bottom: 0;
        }

        &__links {
            display: flex;
            width: 100%;
            justify-content: space-between;

            @include tools.media-breakpoint-up("md") {
                margin-left: auto;
                width: auto;
            }
            a + a {
                margin-left: 22px;
            }
        }
    }

    &__copyright {
        display: flex;
        align-items: center;
        gap: 16px;
        img {
            width: 140px;
            height: auto;
        }
        p,
        small {
            margin-bottom: 0;
            color: rgba(255, 255, 255, 0.55);
        }
    }

    &__links {
        display: flex;
        align-items: center;
        gap: 12px;
    }
}
</style>
