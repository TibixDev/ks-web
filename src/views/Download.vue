<template>
    <div
        id="downloads"
        class="pageview flex flex-col gap-1 relative"
        :class="{ '!overflow-hidden': isContentWarningShown }"
    >
        <div
            v-if="isContentWarningShown"
            id="content-warning"
            class="absolute left-0 top-0 w-full h-full bg-cream text-muted z-10 flex flex-col gap-5 items-center justify-center text-[0.8em]"
        >
            <h2 class="text-3xl text-muted" id="cw-header">{{ t('downloads.cw.header') }}</h2>
            <p class="text-center px-12" v-html="contentWarningLink.includes('/bin/') || contentWarningLink.includes('/steam/') ? t('downloads.cw.warning') : t('downloads.cw.warning_ab')">
            </p>
            <div class="flex flex-row gap-2 items-center">
                <input type="checkbox" name="age-check" id="age-check" v-model="userConsent">
                <label for="age-check">{{ t('downloads.cw.agreement') }}</label>
            </div>
            <div class="flex flex-row gap-4">
                <button
                    class="bg-muted text-cream px-3 py-1 rounded-md generic-hover generic-disabled"
                    :disabled="!userConsent"
                    @click="userConsentConfirm()"
                >
                    {{ t('downloads.cw.submit') }}
                </button>
                <button
                    class="bg-muted text-cream px-3 py-1 rounded-md generic-hover generic-disabled"
                    @click="userConsentDeny()"
                >
                    {{ t('downloads.cw.cancel') }}
                </button>
            </div>
        </div>
        <div id="full-version">
            <h1 class="font-bold">{{ t('downloads.full') }}</h1>
            <div class="separator"></div>
            <i class="text-[0.7em]">{{ t('downloads.dwlanguage')}}: English, Français, Español Internacional, 日本語</i>
            <div class="p-1 text-[0.90em] leading-6">
                <p>
                    <span class="inline-block font-bold w-14 mr-2">Torrent: </span>
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.torrent.windows">Windows</a> |
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.torrent.mac">Mac OS X</a> |
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.torrent.linux">Linux x86</a>
                </p>
                <p>
                    <span class="inline-block font-bold w-14 mr-2">DDL: </span>
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.direct.windows">Windows</a> |
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.direct.mac">Mac OS X</a> |
                    <a @click="onContentSensitiveLink" :href="commonData.downloads.full.direct.linux">Linux x86</a>
                </p>
            <p class="mt-2">
                <i>{{ t('downloads.stores') }}:
                    <a :href="commonData.downloads.full.stores.steam">Steam</a>,
                    <a :href="commonData.downloads.full.stores.itch">itch.io</a>,
                    <a :href="commonData.downloads.full.stores.jastusa">JastUSA</a>.
                </i>
            </p>
            </div>
        </div>
        <div id="act-one-version">
            <h1 class="font-bold">{{ t('downloads.preview') }} (v5)</h1>
            <div class="separator"></div>
            <i class="text-[0.7em] mt-2">{{ t('downloads.dwlanguage')}}: English, Deutsch, Français, Magyar, Italiano, 日本語, Русский, 简体中文, 繁體中文</i>
            <div class="p-1 text-[0.90em] leading-6">
                <p>
                    <span class="inline-block font-bold w-14 mr-2">Torrent: </span>
                    <a :href="commonData.downloads.act1.torrent.windows">Windows</a> |
                    <a :href="commonData.downloads.act1.torrent.mac">Mac OS X</a> |
                    <a :href="commonData.downloads.act1.torrent.linux">Linux x86</a>
                </p>
                <p>
                    <span class="inline-block font-bold w-14 mr-2">DDL: </span>
                    <a :href="commonData.downloads.act1.direct.windows">Windows</a> |
                    <a :href="commonData.downloads.act1.direct.mac">Mac OS X</a> |
                    <a :href="commonData.downloads.act1.direct.linux">Linux x86</a>
                </p>
            </div>
        </div>
        <div id="soundtrack">
            <h1 class="font-bold">{{ t('downloads.soundtrack') }} </h1>
            <div class="separator"></div>
            <div class="p-1 text-[0.90em] leading-6">
                <p>
                    <span class="font-bold">DDL: </span>
                    <a :href="commonData.downloads.soundtrack.direct">Katawa Shoujo Enigmatic Box of Sound</a>
                </p>
            </div>
        </div>
        <div id="artbooks">
            <h1 class="font-bold">{{ t('downloads.artbooks') }}</h1>
            <div class="separator"></div>
            <div class="p-1 text-[0.90em] inline-grid grid-cols-3 gap-3">
                <div v-for="artbook, k of commonData.artbooks" :key="k" class="flex flex-col items-center leading-5" id="artbook-dl">
                    <img
                        :src="`/img/thumbnail/ab/${artbook.thumbnail}`"
                        :alt="`${artbook.title} Thumbnail`"
                    >
                    <h2 class="mt-1">{{ artbook.title }}</h2>
                    <a
                        v-for="language, idx of artbook.languages"
                        :key="idx"
                        :href="artbook.links[idx]"
                        @click="e => ratingCheck(e, k)"
                    >
                        {{ language }}
                    </a>
                </div>
            </div>
        </div>
        <div id="wallpapers">
            <h1 class="font-bold">{{ t('downloads.wallpapers') }}</h1>
            <div class="separator"></div>
            <div class="p-1 text-[0.90em] inline-grid grid-cols-3 gap-3">
                <div v-for="wallpaper, k of commonData.wallpapers" :key="k" class="flex flex-col items-center leading-5">
                    <img
                        :src="`/img/thumbnail/wp/${wallpaper.thumbnail}`"
                        :alt="`${wallpaper.versions[0].split(' ')[0]} Wallpaper Thumbnail`"
                    >
                    <a
                        v-for="version, idx of wallpaper.versions"
                        :key="idx"
                        :href="wallpaper.links[idx]"
                    >
                        {{ version }}
                    </a>
                </div>
            </div>
        </div>
        <div id="link-banners" class="text-[0.90em]">
            <h1 class="font-bold">{{ t('downloads.banners') }}</h1>
            <div class="separator"></div>
            <div class="flex flex-col gap-4">
                <div>
                    <img src="/img/banner/ks_banner_small.jpg" :alt="`${t('downloads.small')} Banner`">
                    <a href="/img/banner/ks_banner_small.jpg">{{ t('downloads.small') }} 88x31</a>
                </div>
                <div>
                    <img src="/img/banner/ks_banner_medium.jpg" :alt="`${t('downloads.medium')} Banner`">
                    <a href="/img/banner/ks_banner_medium.jpg">{{ t('downloads.medium') }} 200x40</a>
                </div>
                <div>
                    <img src="/img/banner/ks_banner.jpg" :alt="`${t('downloads.standard')} Banner`">
                    <a href="/img/banner/ks_banner.jpg">{{ t('downloads.standard') }} 468x60</a>
                </div>
            </div>
        </div>
        <div id="r18-steam" class="text-[0.90em]">
            <h1 class="font-bold">{{ t('downloads.r18.header') }}</h1>
            <div class="separator"></div>
            <p>{{ t('downloads.r18.why') }}</p>
            <p>
                <span class="inline-block font-bold w-18 mr-2">R18 Patch: </span>
                <a @click="onContentSensitiveLink" :href="commonData.downloads.full.stores.r18">{{ t(('downloads.r18.download')) }}</a>
            </p>
            <p><span class="font-bold">{{ t('downloads.r18.instructions.header') }}</span></p>
            <ul class="list-disc">
                <li class="text-black ml-5" v-html="t(('downloads.r18.instructions.download'))"></li>
                <li class="text-black ml-5" v-html="t(('downloads.r18.instructions.navigate'))"></li>
            </ul>
            <div class="p-3">
                <img
                    class="rounded-md"
                    src="/img/r18.webp"
                    :alt="`${t('downloads.r18.instructions.alt')}`"
                >
            </div>
            <p>{{ t('downloads.r18.ack') }}</p>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const isContentWarningShown = ref(false);
const userConsent = ref(false);
const contentWarningLink = ref("");

function onContentSensitiveLink(e: MouseEvent) {
    e.preventDefault();
    const target = e.target as HTMLAnchorElement;
    document.querySelector(".pageview").scrollTop = 0;
    isContentWarningShown.value = true;
    contentWarningLink.value = target.href;
    console.log("[onContentSensitiveLink] Link", contentWarningLink.value);
}

function userConsentConfirm() {
    window.open(contentWarningLink.value, '_blank').focus();
    contentWarningLink.value = "";
    isContentWarningShown.value = false;
    userConsent.value = false;
}

function userConsentDeny() {
    contentWarningLink.value = "";
    isContentWarningShown.value = false;
    userConsent.value = false;
}

const commonData = {
    downloads: {
        full: {
            torrent: {
                windows: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Bwindows%5D%5BA6A47E20%5D.exe.torrent",
                mac: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Bmac%5D%5B1DFC84A6%5D.dmg.torrent",
                linux: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Blinux-x86%5D%5B18161880%5D.tar.bz2.torrent",
            },
            direct: {
                windows: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Bwindows%5D%5BA6A47E20%5D.exe",
                mac: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Bmac%5D%5B1DFC84A6%5D.dmg",
                linux: "https://cdn.fhs.sh/ks/bin/gold_1.3.1/%5B4ls%5D_katawa_shoujo_1.3.1-%5Blinux-x86%5D%5B18161880%5D.tar.bz2",
            },
            stores: {
                steam: "https://store.steampowered.com/app/3068300/Katawa_Shoujo",
                itch: "https://4leafstudios.itch.io/katawa-shoujo",
                jastusa: "https://jastusa.com/games/cc001/katawa-shoujo",
                r18: "https://cdn.fhs.sh/ks/steam/r18.rpa",
            }
        },
        act1: {
            torrent: {
                windows: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bwindows%5D%5BE9193F09%5D.exe.torrent",
                mac: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bmac%5D%5B4392C128%5D.dmg.torrent",
                linux: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Blinux-x86%5D%5B97624142%5D.tar.bz2.torrent",
            },
            direct: {
                windows: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bwindows%5D%5BE9193F09%5D.exe",
                mac: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bmac%5D%5B4392C128%5D.dmg",
                linux: "https://cdn.fhs.sh/ks/bin/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Blinux-x86%5D%5B97624142%5D.tar.bz2",
            }
        },
        soundtrack: {
            direct: "https://cdn.fhs.sh/ks/pr/soundtrack/%5B4ls%5D_katawa_shoujo_enigmatic_box_of_sound_%5B503ACD68%5D.zip"
        }
    },
    artbooks: [
        {
            title: "Player Guide",
            languages: ["Japanese"],
            thumbnail: "tn_kspg.jpg",
            m_content: false,
            links: ["https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Player_Guide_JA.pdf"]
        },
        {
            title: "Fragments of Summer",
            languages: ["Japanese", "English"],
            thumbnail: "tn_fos.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Fragments_of_Summer_JA.pdf",
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Fragments_of_Summer_EN.pdf"
            ]
        },
        {
            title: "Midwinter",
            languages: ["Japanese", "English"],
            thumbnail: "tn_ksmw.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Midwinter_JA.pdf",
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Midwinter_EN.pdf"
            ]
        },
        {
            title: "Tomorrow/Today",
            languages: ["English"],
            thumbnail: "tn_kstt.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Tomorrow_Today_EN.pdf",
            ]
        },
        {
            title: "Kawasoft Artbook",
            languages: ["French"],
            thumbnail: "tn_ksab.jpg",
            m_content: true,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Kawasoft_Artbook.pdf",
            ]
        },
        {
            title: "Imperfect Spectrum",
            languages: ["English"],
            thumbnail: "tn_ksis.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Imperfect_Spectrum_EN.pdf",
            ]
        },
        {
            title: "Beauty & Strangeness",
            languages: ["English"],
            thumbnail: "tn_ksbs.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Beauty_and_Strangeness_EN.pdf",
            ]
        },
        {
            title: "The Soft Hour",
            languages: ["English"],
            thumbnail: "tn_kstsh.png",
            m_content: true,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_The_Soft_Hour_EN.pdf",
            ]
        },
        {
            title: "The Past is Prologue",
            languages: ["Japanese"],
            thumbnail: "tn_kspip.jpg",
            m_content: false,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_The_Past_is_Prologue.pdf",
            ]
        },
        {
            title: "Dangerous",
            languages: ["Japanese"],
            thumbnail: "tn_ksdng.jpg",
            m_content: true,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Shoujo_Dangerous_Artbook.pdf",
            ]
        },
        {
            title: "Katawa Fantasy",
            languages: ["Japanese"],
            thumbnail: "tn_kskf.jpg",
            m_content: true,
            links: [
                "https://cdn.fhs.sh/ks/pr/artbooks/Katawa_Fantasy.pdf"
            ]
        },
    ],
    wallpapers: [
        {
            thumbnail: "misha_tn.jpg",
            versions: ["Misha 1600x1200", "Misha 2560x1600"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/misha_wp_1600x1200.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/misha_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "sd_tn.jpg",
            versions: ["SD Girls 1600x1200", "SD Girls 2560x1600"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/sd_wp_1600x1200.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/sd_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "wizard_tn.jpg",
            versions: ["Wizard 1600x1200", "Wizard 1920x1200"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/wizard_wp_1600x1200.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/wizard_wp_1920x1200.png"
            ]
        },
        {
            thumbnail: "tile_tn.jpg",
            versions: ["Tile 1600x1200", "Tile 2560x1600"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/tile_wp_1600x1200.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/tile_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "shizune_tn.jpg",
            versions: ["Shizune 1024x768", "Shizune 1280x800"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/shizune_wp_1024x768.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/shizune_wp_1280x800.png"
            ]
        },
        {
            thumbnail: "soviet_tn.jpg",
            versions: ["Soviet 1600x1200", "Soviet 2560x1600"],
            links: [
                "https://cdn.fhs.sh/ks/pr/wallpapers/soviet_wp_1600x1200.png",
                "https://cdn.fhs.sh/ks/pr/wallpapers/soviet_wp_2560x1600.png"
            ]
        },
    ]
}

const artbookRating = commonData.artbooks;

function ratingCheck (e: MouseEvent, n: any) {
    console.log("Rating check running!")
    if (artbookRating[n].m_content == true) {
        onContentSensitiveLink(e);
    }
}
</script>

<style>
#cw-header {
    font-family: Playtime;
}

.mono-code {
    @apply font-mono bg-black/10 p-0.5 rounded-md text-[#6b2323];
}
</style>
