# sps

> [!WARNING]
> I will scrap this project in favor of sps v2 some time in the future (when v2 is built and ready which might take a while). The reason is that I am planning to
> implement my own packaging system, my own version of atomic installs / updated complete with automatic snapshots and full, down to single package rollbacks +
> automatic cve checks and some other stuffs. After a lot of thinking and looking at Homebrew's architecture I've come to the conclusion that I do not like it (burn
> me for it ;). Defining my own build system will allow for a more performant and maintainable system in the long run. (Just a bit anxious about how to host packages
> / do all the repo stuff. Like really anxious but I'll figure it out)
>
> Another reason is that I made some choices on internal architecture in the beginning that I have come to see as suboptimal but can not easily refactor so this will
> allow me to go for the better option right from the get go (go for rx/tx for status propagation from the start, build the core fully async etc.)
>
> I have just made the repo for sps2 public. There is no repositories yet and core systems still do not work and need debugging. However it passes ci and the
> architecture is largely in place. I will have to create a automatic upstream tracking system, automatic builds and create build scripts for the most important
> tools too still + bootstrap the repositories.
>
> Never done that so if anyone has experience with that stuff help is appreciated. 
>
> For repo architecture I will probably go for a classic unix style repo format with cloudflare r2 and automatic replication to multiple regions. Well that is quite
> far out. Still it is coming along well, just built my first package with it. Found some small issues with install right after and am working on those now.
>
> https://github.com/alexykn/sps2 Take a look if you want!


sps is a next‑generation, Rust‑powered package manager inspired by Homebrew. It installs and manages:

- **Formulae:** command‑line tools, libraries, and languages
- **Casks:** desktop applications and related artifacts on macOS

> _ARM only for now, might add x86 support eventually_

---

## ⚙️ Project Structure

- **sps‑core** Core library: fetching, dependency resolution, archive extraction, artifact handling (apps, binaries, pkg installers, fonts, plugins, zap/preflight/uninstall stanzas, etc.)

- **sps‑cli** Command‑line interface: `sps` executable wrapping the core library.

---

## 🚧 Current Status

- Bottle installation and uninstallation
- Cask installation and uninstallation
- Reinstall command for reinstalls
- Upgrade command for updates (Casks deactivated at the moment)
- Parallel downloads and installs for speed
- Automatic dependency resolution and installation
- Building Formulae from source (very early impl)

---

## 🚀 Roadmap

- **Cleanup** old downloads, versions, caches
- **Prefix isolation:** support `/opt/sps` as standalone layout
- **`sps init`** helper to bootstrap your environment
- **Ongoing** Bug fixes and stability improvements

---

## Trying it out:

```bash
cargo install sps
```
> due too the amount of work keeping the crates up to date with every change would entail the crates.io published version will only be updated after major changes or fixes (if there are none expect once a week)
---

<img width="1242" alt="Screenshot 2025-05-24 at 10 09 03" src="https://github.com/user-attachments/assets/eac4bb5e-5447-48a6-b202-062ba382ce0c" />

<img width="1242" alt="Screenshot 2025-05-24 at 10 09 49" src="https://github.com/user-attachments/assets/c82ad6be-a286-48ce-9d9f-8b26216e7f48" />

---

## 📦 Usage

```sh
# Print help
sps --help

# Update metadata
sps update

# List all installed packages
sps list

# List only installed formulae
sps list --formula

# List only installed casks
sps list --cask

# Search for packages
sps search <formula/cask>

# Get package info
sps info <formula/cask>

# Install bottles or casks
sps install <formula/cask>

# Build and install a formula from source
sps install --build-from-source <formula>

# Uninstall
sps uninstall <formula/cask>

# Reinstall
sps reinstall <formula/cask>

#Upgrade
sps upgrade <formula/cask> or --all

# (coming soon)
sps cleanup
sps init
```

-----

## 🏗️ Building from Source

**Prerequisites:** Rust toolchain (stable).

```sh
git clone <repo-url>
cd sps
cargo build --release
```

The `sps` binary will be at `target/release/sps`. Add it to your `PATH`.


-----

## 📥 Using the Latest Nightly Build

You can download the latest nightly build from [`actions/workflows/rust.yml`](../../actions/workflows/rust.yml) inside this repository (select a successful build and scroll down to `Artifacts`).

After extracting the downloaded archive, you can run the binary directly:

```sh
./sps --help
```


-----

## 🤝 Contributing

sps lives and grows by your feedback and code\! We’re particularly looking for:

  - Testing and bug reports for Cask & Bottle installation + `--build-from-source`
  - Test coverage for core and cask modules
  - CLI UI/UX improvements
  - See [CONTRIBUTING.md](CONTRIBUTING.md)

Feel free to open issues or PRs. Every contribution helps\!

-----

## 📄 License

  - **sps:** BSD‑3‑Clause - see [LICENSE.md](LICENSE.md)
  - Inspired by Homebrew BSD‑2‑Clause — see [NOTICE.md](NOTICE.md)

-----

> *Alpha software. No guarantees. Use responsibly.*
