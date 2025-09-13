# Publish
```
mcp-publisher init
mcp-publisher login github
openssl genpkey -algorithm Ed25519 -out key.pem
echo "gepuro.net. IN TXT \"v=MCPv1; k=ed25519; p=$(openssl pkey -in key.pem -pubout -outform DER | tail -c 32 | base64)\""
mcp-publisher login dns --domain gepuro.net --private-key $(openssl pkey -in key.pem -noout -text | grep -A3 "priv:" | tail -n +2 | tr -d ' :\n')
mcp-publisher publish
curl "https://registry.modelcontextprotocol.io/v0/servers?search=net.gepuro.mcp-company-lens-v1/company-lens-mcp-registry"
```