# 🌼 GitHub Action to Setup Huawei Cloud KooCLI - `hcloud` CLI

[![🧪 Testing](https://github.com/vbem/setup-hcloud/actions/workflows/test.yml/badge.svg)](https://github.com/vbem/setup-hcloud/actions/workflows/test.yml)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/vbem/setup-hcloud?label=Release&logo=github)](https://github.com/vbem/setup-hcloud/releases)
[![Marketplace](https://img.shields.io/badge/GitHub%20Actions-Marketplace-blue?logo=github)](https://github.com/marketplace/actions/setup-hcloud)

## About

[***KooCLI***](https://support.huaweicloud.com/hcli/index.html) is the Huawei Cloud official command-line tool. Huawei Cloud previously provided a [simple setup action](https://github.com/huaweicloud/huaweicloud-cli-action), but that repository now returns 404. This action provides an alternative way to setup *KooCLI* on your runner. It supports Linux, macOS, and Windows runners, and can download *KooCLI* binaries from an internal mirror when needed.

## Example usage

```yaml
- name: Setup Huawei Cloud KooCLI
  uses: vbem/setup-hcloud@hash

- name: Test KooCLI by querying the current IAM caller
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
`agree-privacy` | Boolean | `true` | Whether to accept the [privacy statement](https://support.huaweicloud.com/productdesc-hcli/hcli_024.html) during installation.
`check-version` | Boolean | `true` | Whether to check the [KooCLI version](https://support.huaweicloud.com/usermanual-hcli/hcli_04_004.html) after installation. This requires `agree-privacy` to be `true`.
`mirror` | String | `""` | The mirror URL prefix used to download KooCLI. Default is empty, which will use the official mirrors: the [Singapore mirror](https://support.huaweicloud.com/intl/en-us/qs-hcli/hcli_02_003.html) for GitHub-hosted runners, and the [Beijing mirror](https://support.huaweicloud.com/qs-hcli/hcli_02_003.html) otherwise.

## Outputs

ID | Type | Description | Example
--- | --- | --- | ---
`url` | String | The URL used to download the KooCLI package. | `https://cn-north-4-hdn-koocli.obs.cn-north-4.myhuaweicloud.com/cli/latest/huaweicloud-cli-linux-amd64.tar.gz`
`path` | String | The path to the KooCLI binary on the runner. | `/usr/local/bin/hcloud`
`version` | String | The detected KooCLI version. | `Current KooCLI version: 7.2.2`
