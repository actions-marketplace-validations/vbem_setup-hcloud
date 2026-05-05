# 🌼 GitHub Action to Setup Huawei Cloud KooCLI - `hcloud` CLI

[![🧪 Testing](https://github.com/vbem/setup-hcloud/actions/workflows/test.yml/badge.svg)](https://github.com/vbem/setup-hcloud/actions/workflows/test.yml)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/vbem/setup-hcloud?label=Release&logo=github)](https://github.com/vbem/setup-hcloud/releases)
[![Marketplace](https://img.shields.io/badge/GitHub%20Actions-Marketplace-blue?logo=github)](https://github.com/marketplace/actions/setup-hcloud)

## About

The [***KooCLI***](https://support.huaweicloud.com/hcli/index.html) is the official command-line tool provided by Huawei Cloud. It once provided an [official simple installation action](https://github.com/huaweicloud/huaweicloud-cli-action), but it is currently giving a 404 error for unknown reasons. This repository provides an alternative GitHub Action to install KooCLI in your workflow. It supports both Linux/macOS and Windows runners, and allows you to specify your internal mirror for downloading KooCLI binaries if needed.

## Example usage

```yaml
- name: Setup HW Cloud KooCLI
  uses: vbem/setup-hcloud@main

- name: Test CLI by HW Cloud STS service
  env:
    HUAWEICLOUD_SDK_REGION: cn-north-4
    HUAWEICLOUD_SDK_AK: ${{ secrets.HUAWEICLOUD_SDK_AK }}
    HUAWEICLOUD_SDK_SK: ${{ secrets.HUAWEICLOUD_SDK_SK }}
  run: |
    hcloud sts GetCallerIdentity \
        --cli-region="${HUAWEICLOUD_SDK_REGION}" \
        --cli-access-key="${HUAWEICLOUD_SDK_AK}" \
        --cli-secret-key="${HUAWEICLOUD_SDK_SK}" \
        | jq -C
```

## Inputs

ID | Type | Default | Description
--- | --- | --- | ---
`agree-privacy` | Boolean | `true` | Whether to agree [privacy statement](https://support.huaweicloud.com/productdesc-hcli/hcli_024.html) when installing KooCLI.
`check-version` | Boolean | `true` | Whether to check [KooCLI version](https://support.huaweicloud.com/usermanual-hcli/hcli_04_004.html) after installation (must work with `agree-privacy`).
`base-url` | String | `https://cn-north-4-hdn-koocli.obs.cn-north-4.myhuaweicloud.com/cli/latest/` | Base URL for downloading [KooCLI official binaries](https://support.huaweicloud.com/qs-hcli/hcli_02_003_02.html). You can set it to your internal mirror if needed.

## Outputs

ID | Type | Description | Example
--- | --- | --- | ---
`url` | String | The URL used to download KooCLI binary. | `https://cn-north-4-hdn-koocli.obs.cn-north-4.myhuaweicloud.com/cli/latest/huaweicloud-cli-linux-amd64.tar.gz`
`path` | String | Path to KooCLI binary in the runner. | `/usr/local/bin/hcloud`
`version` | String | The checked KooCLI version. | `Current KooCLI version: 7.2.2`
