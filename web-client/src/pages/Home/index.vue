<script setup>
import ClaimControls from './ClaimControls.vue'
import ConnectWallet from './ConnectWallet.vue'
import DaoLogo from '../../components/ui/DaoLogo.vue'
import Preview from './Preview.vue'
import PreviewControls from './PreviewControls.vue'
import usePreviewState from './usePreviewState'
import useRouteParameterSync from './useRouteParameterSync'
import { provide } from 'vue'
import { PIXEL_AVATAR_NETWORK } from '../../constants'

const networkConfigured = PIXEL_AVATAR_NETWORK.chainId > 0
const previewState = usePreviewState()

useRouteParameterSync(previewState)

provide('previewState', previewState)
</script>

<template>
    <div class="min-h-screen flex flex-col sm:flex-row">
        <div class="sm:w-2/5 bg-white py-10 px-4 flex">
            <div
                class="
                    flex flex-col
                    items-center
                    justify-center
                    space-y-10
                    w-full
                    max-w-md
                    mx-auto
                "
            >
                <div
                    class="flex items-center w-full"
                    :class="
                        networkConfigured ? 'justify-between' : 'justify-around'
                    "
                >
                    <DaoLogo class="w-16 h-16 rounded-full shadow-md" />

                    <ConnectWallet v-if="networkConfigured" />
                </div>

                <ClaimControls />

                <PreviewControls />
            </div>
        </div>

        <div class="sm:w-3/5 bg-gray-100 border-l border-gray-200">
            <div class="flex flex-col sm:min-h-screen sm:sticky sm:top-0">
                <div class="-mb-10 flex-1 flex items-center justify-center">
                    <Preview :state="previewState" class="flex-1 max-w-md" />
                </div>

                <div class="flex justify-end p-4">
                    <a
                        target="_blank"
                        title="Github"
                        href="https://github.com/Developer-DAO/pixel-avatars"
                        class="flex items-center space-x-3"
                    >
                        <span class="text-sm">View on Github</span>
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            width="48"
                            height="48"
                            viewBox="0 0 24 24"
                        >
                            <path
                                d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                            />
                        </svg>
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>