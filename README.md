# 📝 Notes

Nested tables are supported: if you add a table, Soap will recursively clean its contents.
Cleanup() is safe to call multiple times — it won't error on an already-empty instance.
Destroy() should be called when the Soap instance itself is no longer needed.
