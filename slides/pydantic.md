## Pydantic Settings

```python
from pydantic_settings import BaseSettings
from pydantic import Field, SecretStr

class UserSettings(BaseSettings):
    user: str
    password: SecretStr

class Settings(BaseSettings):
    app_name: str = "My Cool App"
    debug: bool = Field(default=False, env="DEBUG")
    port: int = 8000
    user: UserSettings
    class Config:
        env_file = ".env"  # optional
...

settings = Settings()
print(settings.app_name)
print(settings.debug)