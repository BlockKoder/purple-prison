<template>
    <Modal v-model="isOpen" width="440px">
        <div class="username-modal">
            <div class="username-modal__header">
                <div class="username-modal__avatar">
                    <img
                        :src="`https://mc-heads.net/avatar/${usernameInput.trim() || 'Steve'}/64`"
                        alt="Minecraft Avatar"
                        loading="lazy"
                    />
                </div>
                <h3>Minecraft Username</h3>
                <p>
                    Enter your Minecraft username to view packages & add items
                    to your cart.
                </p>
            </div>

            <form @submit.prevent="handleSubmit" class="username-modal__form">
                <Input
                    v-model="usernameInput"
                    placeholder="e.g. Notch"
                    label="In-Game Username"
                    required
                />

                <p v-if="errorMessage" class="username-modal__error">
                    {{ errorMessage }}
                </p>

                <Button
                    type="submit"
                    :disabled="!usernameInput.trim() || isLoading"
                    :loading="isLoading"
                    class="w-100 mt-4"
                >
                    Continue
                </Button>
            </form>
        </div>
    </Modal>
</template>

<script setup lang="ts">
const uiStore = useUIStore();
const authStore = useAuthStore();
const toastStore = useToastStore();

const isOpen = computed({
    get: () => uiStore.isItemActive("username-modal"),
    set: (val) => uiStore.toggleItem("username-modal", val),
});

const usernameInput = ref("");
const isLoading = ref(false);
const errorMessage = ref("");

watch(isOpen, (open) => {
    if (open && authStore.isAuthenticated && authStore.user?.username) {
        usernameInput.value = authStore.user.username;
    }
});

const handleSubmit = async () => {
    const trimmed = usernameInput.value.trim();
    if (!trimmed) return;

    isLoading.value = true;
    errorMessage.value = "";

    try {
        await authStore.login(trimmed);
        toastStore.addToast(`Logged in as ${trimmed}`, { type: "success" });
        isOpen.value = false;
    } catch (err: unknown) {
        const error = err as Error;
        errorMessage.value =
            error?.message || "Failed to set username. Please try again.";
    } finally {
        isLoading.value = false;
    }
};
</script>

<style scoped lang="scss">
.username-modal {
    padding: 10px 16px;

    &__header {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        margin-bottom: 20px;

        h3 {
            margin: 12px 0 6px;
            color: #fff;
            font-family: Orbitron, sans-serif;
            font-size: 20px;
            text-transform: uppercase;
        }

        p {
            color: rgba(255, 255, 255, 0.65);
            font-size: 14px;
            line-height: 1.5;
            margin: 0;
        }
    }

    &__avatar {
        width: 72px;
        height: 72px;
        border-radius: 12px;
        padding: 4px;
        background: rgba(242, 202, 80, 0.15);
        border: 2px solid #f2ca50;
        box-shadow: 0 0 20px rgba(242, 202, 80, 0.25);
        display: flex;
        align-items: center;
        justify-content: center;

        img {
            width: 100%;
            height: 100%;
            border-radius: 8px;
            object-fit: cover;
            image-rendering: pixelated;
        }
    }

    &__form {
        width: 100%;
    }

    &__error {
        margin-top: 10px;
        color: #ef4444;
        font-size: 13px;
        text-align: center;
    }
}
</style>
