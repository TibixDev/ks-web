<template>
    <footer class="grid grid-cols-6 w-full p-2">
        <div id="copyright" class="col-span-4 sm:col-span-2 order-3 sm:order-[unset]">
            <img src="/img/4lsl.webp" alt="Four Leaf Studios Logo">
            <p class="leading-5 mt-2">
                © 2007-2024
                <a href="mailto:staff@katawa-shoujo.com">Four Leaf Studios</a><br>
                © 2024
                <a href="https://fhs.sh">Fleeting Heartbeat Studios</a> and contributors<br>
                The code is available under the <a href="https://codeberg.org/fhs/ks-web/src/branch/main/LICENSE">MIT License</a>
            </p>
        </div>
        <div id="languages" class="col-span-6 sm:col-span-2 flex items-end justify-center mb-12 sm:mb-0">
            <div class="flex flex-row items-center justify-center flex-wrap gap-0 w-[400px]">
                <div v-for="language, k of languages" :key="k" class="flex flex-row items-center">
                    <a href="#" @click="changeLocale(language.code)">
                        {{ language.name }}
                    </a>
                    <div v-if="k != languages.length - 1" class="h-[1rem] w-[1px] bg-muted mx-[0.4em]"></div>
                </div>
            </div>
        </div>
        <div id="notices" class="col-span-2 order-3 sm:order-[unset] sm:col-span-2 flex flex-col gap-2 items-end justify-end">
            <a target="_blank" href="https://twitter.com/fourleafstudios?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="small" data-show-screen-name="false" data-show-count="false">Follow @fourleafstudios</a>
            <a target="_blank" href="https://creativecommons.org/licenses/by-nc-nd/3.0/">
                <img src="/img/cc_by_nc_nd_80x15.webp" alt="CC by NC-ND license">
            </a>
        </div>
    </footer>
</template>


<script setup lang="ts">
import { useI18n } from 'vue-i18n';
import { persistentChangeLocale } from '@/i18n/provider';

const { t, locale } = useI18n({ useScope: 'global' })

const languages = [
    { name: "Česky", code: "cs" },
    { name: "Deutsch", code: "de" },
    { name: "Español", code: "es" },
    { name: "English", code: "en" },
    { name: "Suomi", code: "fi" },
    { name: "Français", code: "fr" },
    { name: "Magyar", code: "hu" },
    { name: "Italiano", code: "it" },
    { name: "日本語", code: "ja" },
    { name: "한국말", code: "ko" },
    { name: "Português", code: "pt" },
	{ name: "Português Brasileiro", code: "pt-BR" },
    { name: "Русский", code: "ru" },
    { name: "中文(简体)", code: "zh" },
    { name: "中文(繁體)", code: "zh-TW" }
]

function changeLocale(newLocale: string) {
    persistentChangeLocale(locale, newLocale);
}
</script>

<style scoped>
footer {
    font-family: sans-serif;
    font-size: 12px;
}

a:hover {
    color: #111111;
}

.break {
    flex-basis: 100%;
    height: 0;
}
</style>
