# npe2api

The REST API used by napari, the napari plugin manager and
[napari-hub.org](https://napari-hub.org) to query plugins.

The endpoint for the API is: <https://api.napari.org>

It is a static site served from Cloudflare. Every two hours a GitHub Action
fetches plugin data, commits it to the `data` branch, and deploys it; see
[CONTRIBUTING.md](./CONTRIBUTING.md#how-this-repo-works).

## Endpoints

| Type             | Endpoint                                                             | Note                                             |
|------------------|----------------------------------------------------------------------|--------------------------------------------------|
| Plugin index     | [/api/plugins](https://api.napari.org/api/plugins)                   |                                                  |
| Summary info     | [/api/extended_summary](https://api.napari.org/api/extended_summary) |                                                  |
| PyPI information |                                                                      | For an individual plugin: /api/pypi/{pypi_name}  |
| Conda index      | [/api/conda-map](https://api.napari.org/api/conda-map)               | For an individual plugin: /api/conda/{pypi_name}. `/api/conda` is the deprecated name. |
| Readers          | [/api/readers](https://api.napari.org/api/readers)                   | Filename pattern to reader                       |
| Fetch errors     | [/errors.json](https://api.napari.org/errors.json)                   |                                                  |
| Manifests        | For an individual manifest: /api/manifest/{plugin_name}              |                                                  |
| Badge            | For a shields.io badge: /api/shields/{plugin_name}                   | `https://img.shields.io/endpoint?url=https://api.napari-hub.org/shields/{plugin_name}` |

Plugin names may be given in any spelling (`Napari_Foo` finds `napari-foo`).
An unknown plugin is a 404 with a JSON `error`.

## Contributing

If you are interested in contributing to this repo, see the [CONTRIBUTING.md](./CONTRIBUTING.md) page.

## Code of conduct

`npe2api` is maintained by the [napari](https://napari.org/) community. The `napari` community has a [Code of Conduct](https://napari.org/dev/community/code_of_conduct.html) that should be honored by everyone who participates in the `napari` community.
