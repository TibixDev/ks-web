<template>
    <div id="downloads" class="pageview flex flex-col gap-1">
        <div id="full-version">
            <h1 class="font-bold">Full Version</h1>
            <div class="separator"></div>
            <i class="text-[0.7em]">Languages: English, Français, Español Internacional, 日本語</i>
            <div class="p-1 text-[0.90em] leading-6">
                <p>
                    <span class="inline-block font-bold w-14 mr-2">Torrent: </span>
                    <a :href="commonData.downloads.full.torrent.windows">Windows</a> |
                    <a :href="commonData.downloads.full.torrent.mac">Mac OS X</a> |
                    <a :href="commonData.downloads.full.torrent.linux">Linux x86</a>
                </p>
                <p>
                    <span class="inline-block font-bold w-14 mr-2">DDL: </span>
                    <a :href="commonData.downloads.full.direct.windows">Windows</a> |
                    <a :href="commonData.downloads.full.direct.mac">Mac OS X</a> |
                    <a :href="commonData.downloads.full.direct.linux">Linux x86</a>
                </p>
            </div>
        </div>
        <div id="act-one-version">
            <h1 class="font-bold">Act 1 (v5)</h1>
            <div class="separator"></div>
            <i class="text-[0.7em] mt-2">Languages: English, Deutsch, Français, Magyar, Italiano, 日本語, Русский, 简体中文, 繁體中文</i>
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
            <h1 class="font-bold">Soundtrack</h1>
            <div class="separator"></div>
            <div class="p-1 text-[0.90em] leading-6">
                <p>
                    <span class="font-bold">DDL: </span>
                    <a :href="commonData.downloads.soundtrack.direct">Katawa Shoujo Enigmatic Box of Sound</a>
                </p>
            </div>
        </div>
        <div id="artbooks">
            <h1 class="font-bold">Artbooks</h1>
            <div class="separator"></div>
            <div class="p-1 text-[0.90em] inline-grid grid-cols-3 gap-3">
                <div v-for="artbook, k of commonData.artbooks" :key="k" class="flex flex-col items-center leading-5">
                    <img
                        :src="`/img/thumbnail/ab/${artbook.thumbnail}`"
                        :alt="`${artbook.title} Thumbnail`"
                    >
                    <h2 class="mt-1">{{ artbook.title }}</h2>
                    <a
                        v-for="language, idx of artbook.languages"
                        :key="idx"
                        :href="artbook.links[idx]"
                    >
                        {{ language }}
                    </a>
                </div>
            </div>
        </div>
        <div id="wallpapers">
            <h1 class="font-bold">Wallpapers</h1>
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
            <h1 class="font-bold">Link Banners</h1>
            <div class="separator"></div>
            <div class="flex flex-col gap-4">
                <div>
                    <img src="/img/banner/ks_banner_small.jpg" alt="Small Banner">
                    <a href="/img/banner/ks_banner_small.jpg">Small 88x31</a>
                </div>
                <div>
                    <img src="/img/banner/ks_banner_medium.jpg" alt="Medium Banner">
                    <a href="/img/banner/ks_banner_medium.jpg">Medium 200x40</a>
                </div>
                <div>
                    <img src="/img/banner/ks_banner.jpg" alt="Standard Banner">
                    <a href="/img/banner/ks_banner.jpg">Standard 468x60</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n';
const { t } = useI18n();

const commonData = {
    downloads: {
        full: {
            torrent: {
                windows: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5bwindows%5d%5bA6A47E20%5d.exe.torrent",
                mac: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5bmac%5d%5b1DFC84A6%5d.dmg.torrent",
                linux: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5blinux-x86%5d%5b18161880%5d.tar.bz2.torrent",
            },
            direct: {
                windows: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5bwindows%5d%5bA6A47E20%5d.exe",
                mac: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5bmac%5d%5b1DFC84A6%5d.dmg",
                linux: "http://www.katawa-shoujo.com/res/shrinkwrap.php?link=gold_1.3.1/%5b4ls%5d_katawa_shoujo_1.3.1-%5blinux-x86%5d%5b18161880%5d.tar.bz2",
            }
        },
        act1: {
            torrent: {
                windows: "http://dl.katawa-shoujo.com/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bwindows%5D%5BE9193F09%5D.exe.torrent",
                mac: "http://dl.katawa-shoujo.com/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bmac%5D%5B4392C128%5D.dmg.torrent",
                linux: "http://dl.katawa-shoujo.com/a1v5/%5B4ls%5D_katawa_shoujo_act1_v5_%5Blinux-x86%5D%5B97624142%5D.tar.bz2.torrent",
            },
            direct: {
                windows: "http://dl.katawa-shoujo.com/a1v5/mirrors/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bwindows%5D%5BE9193F09%5D.exe",
                mac: "http://dl.katawa-shoujo.com/a1v5/mirrors/%5B4ls%5D_katawa_shoujo_act1_v5_%5Bmac%5D%5B4392C128%5D.dmg",
                linux: "http://dl.katawa-shoujo.com/a1v5/mirrors/%5B4ls%5D_katawa_shoujo_act1_v5_%5Blinux-x86%5D%5B97624142%5D.tar.bz2",
            }
        },
        soundtrack: {
            direct: "http://dl.katawa-shoujo.com/pr/soundtrack/%5b4ls%5D_katawa_shoujo_enigmatic_box_of_sound_%5b503ACD68%5D.zip"
        }
    },
    artbooks: [
        {
            title: "Player Guide",
            languages: ["Japanese"],
            thumbnail: "tn_kspg.jpg",
            links: ["http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Player_Guide_JA.pdf"]
        },
        {
            title: "Fragments of Summer",
            languages: ["Japanese", "English"],
            thumbnail: "tn_fos.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Fragments_of_Summer_JA.pdf",
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Fragments_of_Summer_EN.pdf"
            ]
        },
        {
            title: "Midwinter",
            languages: ["Japanese", "English"],
            thumbnail: "tn_ksmw.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Midwinter_JA.pdf",
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Midwinter_EN.pdf"
            ]
        },
        {
            title: "Tomorrow/Today",
            languages: ["English"],
            thumbnail: "tn_kstt.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Tomorrow_Today_EN.pdf",
            ]
        },
        {
            title: "Kawasoft Artbook",
            languages: ["French"],
            thumbnail: "tn_ksab.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Kawasoft_Artbook.pdf",
            ]
        },
        {
            title: "Imperfect Spectrum",
            languages: ["English"],
            thumbnail: "tn_ksis.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Imperfect_Spectrum_EN.pdf",
            ]
        },
        {
            title: "Beauty & Strangeness",
            languages: ["English"],
            thumbnail: "tn_ksbs.jpg",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_Beauty_and_Strangeness_EN.pdf",
            ]
        },
        {
            title: "The Soft Hour",
            languages: ["English"],
            thumbnail: "tn_kstsh.png",
            links: [
                "http://dl.katawa-shoujo.com/pr/artbooks/Katawa_Shoujo_The_Soft_Hour_EN.pdf",
            ]
        },

    ],
    wallpapers: [
        {
            thumbnail: "misha_tn.jpg",
            versions: ["Misha 1600x1200", "Misha 2560x1600"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/misha_wp_1600x1200.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/misha_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "sd_tn.jpg",
            versions: ["SD Girls 1600x1200", "SD Girls 2560x1600"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/sd_wp_1600x1200.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/sd_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "wizard_tn.jpg",
            versions: ["Wizard 1600x1200", "Wizard 1920x1200"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/wizard_wp_1600x1200.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/wizard_wp_1920x1200.png"
            ]
        },
        {
            thumbnail: "tile_tn.jpg",
            versions: ["Tile 1600x1200", "Tile 2560x1600"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/tile_wp_1600x1200.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/tile_wp_2560x1600.png"
            ]
        },
        {
            thumbnail: "shizune_tn.jpg",
            versions: ["Shizune 1024x768", "Shizune 1280x800"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/shizune_wp_1024x768.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/shizune_wp_1280x800.png"
            ]
        },
        {
            thumbnail: "soviet_tn.jpg",
            versions: ["Soviet 1600x1200", "Soviet 2560x1600"],
            links: [
                "http://dl.katawa-shoujo.com/pr/wallpapers/soviet_wp_1600x1200.png",
                "http://dl.katawa-shoujo.com/pr/wallpapers/soviet_wp_2560x1600.png"
            ]
        },
    ]
}
</script>

<style>
</style>