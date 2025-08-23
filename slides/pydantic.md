
# Pydantic Settings

load settings from environment variables with types

<v-clicks>

````md magic-move

```python{|4|5|6|10}
import os, json

DEBUG = os.getenv("DEBUG", "").lower() in ("1","true","yes","y")
PORT = int(os.getenv("PORT", "8000"))
ALLOWED_HOSTS = json.loads(os.getenv("ALLOWED_HOSTS", "[]"))
API_KEY = os.getenv("API_KEY", "")

print(f"port={PORT}", f"debug={DEBUG}", 
      f"hosts={ALLOWED_HOSTS}", 
      "api_key=" + "**********" if API_KEY else "")
```
```python{4|7|9|11}
from pydantic_settings import BaseSettings, SettingsConfigDict
from pydantic import SecretStr

class Settings(BaseSettings):
    debug: bool = False
    port: int = 8000
    allowed_hosts: list[str] = []
    api_key: SecretStr
    model_config = SettingsConfigDict(env_file=".env")  # optional!

s = Settings()
print(s.app_name, f"port={s.port}", f"debug={s.debug}", f"hosts={s.allowed_hosts}", 
      f"api_key={s.api_key}")
```
````
</v-clicks>


