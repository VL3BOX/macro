<template>
    <div class="m-list-nav">
        <h5 class="u-title">
            {{ $t('心法导航') }}
            <router-link class="u-more" :to="{ query: { subtype: '' } }"
                >{{ $t('全部心法') }}<i class="el-icon-arrow-right"></i
            ></router-link>
        </h5>
        <ul class="m-macro-nav u-list">
            <li class="u-item" v-for="(item, i) in xfmaps" :key="i" v-show="item.client.includes(client)">
                <router-link class="u-link" :to="{ query: { subtype: item.name } }" :class="{ on: isActive(item) }">
                    <i class="u-pic">
                        <img :src="showMountIcon(item.id)" :alt="item.name" />
                    </i>
                    <span class="u-txt">{{ $t(item.name) }}</span> <!-- i18n: school name -->
                </router-link>
            </li>
        </ul>

        <h5 class="u-title">{{ $t('在线应用') }}</h5>
        <div class="m-nav-group">
            <a href="/pz" target="_blank">
                <img class="u-icon" :src="getAppIcon('pz', true)" />
                <span>{{ $t('配装模拟器') }}</span>
                <em>Assembly Simulator</em>
            </a>
            <a href="/macro/talent" target="_blank" v-if="client == 'std'">
                <img class="u-icon" :src="getAppIcon('talent', true)" />
                <span>{{ $t('奇穴模拟器') }}</span>
                <em>Talent Simulator</em>
            </a>
            <a href="/macro/talent2" target="_blank" v-else>
                <img class="u-icon" :src="getAppIcon('talent', true)" />
                <span>{{ $t('镇派模拟器') }}</span>
                <em>Talent Simulator</em>
            </a>
            <a href="/macro/macroeditor" target="_blank">
                <img class="u-icon" :src="getAppIcon('macroeditor', true)" />
                <span>{{ $t('云宏编辑器') }}</span>
                <em>Macro Editor</em>
            </a>
        </div>
    </div>
</template>

<script>
import xfmap from "@jx3box/jx3box-data/data/xf/xf.json";
import { __imgPath } from "@jx3box/jx3box-common/data/jx3box.json";
import { getAppIcon, showMountIcon } from "@jx3box/jx3box-common/js/utils";
export default {
    name: "list_nav",
    computed: {
        client: function () {
            return this.$store.state.client;
        },
        xfmaps() {
            delete xfmap["山居剑意"];
            return xfmap;
        },
    },
    methods: {
        isActive: function (item) {
            return item.name == this.$route.query.subtype;
        },
        getAppIcon,
        showMountIcon,
    },
};
</script>

<style lang="less">
@import "~@/assets/css/nav.less";
</style>
