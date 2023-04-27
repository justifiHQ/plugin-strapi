<template>
    <div class="strapi-settings-edit">
        <wwEditorFormRow required label="URL">
            <wwEditorInputText
                type="text"
                name="url"
                placeholder="https://my-strapi-url.com"
                :model-value="settings.privateData.url"
                large
                @update:modelValue="saveUrl"
            />
        </wwEditorFormRow>
        <wwEditorFormRow required label="API Key">
                <wwEditorInputText
                    type="password"
                    name="apikey"
                    placeholder="**************"
                    :model-value="settings.privateData.apikey"
                    large
                    @update:modelValue="saveKey"
                />
            </wwEditorFormRow>
    </div>
</template>

<script>
export default {
    props: {
        settings: { type: Object, required: true },
    },
    emits: ['update:settings'],
    methods: {
        saveUrl(value) {
            this.setPrivateProp('url', value.trim().replace(/\/+$/g, ''));
        },
        saveKey(value){
            this.setPrivateProp('apikey', value.trim());
        },
        setPrivateProp(key, value) {
            this.$emit('update:settings', {
                ...this.settings,
                privateData: { ...this.settings.privateData, [key]: value },
            });
        },
    },
};
</script>

<style lang="scss" scoped>
.strapi-settings-edit {
    &__link {
        color: var(--ww-color-blue-500);
        margin-left: var(--ww-spacing-02);
    }
}
</style>
