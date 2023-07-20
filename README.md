# nhost-run-config-deploy
Deploys Nhost Run Configuration

## Usage

Use this action to deploy configuration to an Nhost Run Service. Example:

```
```yaml
    - name: Install Nhost CLI
      id: install-nhost-cli
      uses: nhost-actions/install-nhost-cli@v1

    - name: Authenticate with Nhost
      uses: nhost-actions/authenticate@v1
      with:
        pat: ${{ secrets.NHOST_PAT }}

    - name: Configure docker credentials
      uses: nhost-actions/configure-container-registry@v1

    - name: Set up QEMU
      uses: docker/setup-qemu-action@v2

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2

    - name: Build and push
      uses: docker/build-push-action@v4
      with:
        context: .
        platforms: linux/amd64,linux/arm64
        push: true
        tags: registry.eu-central-1.nhost.run/8e00eb02-1e53-40a9-9607-604ad199517d:${{ github.sha }}

    - name: Configure docker credentials
      uses: nhost-actions/nhost-run-config-deploy@v1
      with:
       configuration_file: nhost-service.toml
       service_id: 8e00eb02-1e53-40a9-9607-604ad199517d
       image: registry.eu-central-1.nhost.run/8e00eb02-1e53-40a9-9607-604ad199517d:${{ github.sha }}
```
