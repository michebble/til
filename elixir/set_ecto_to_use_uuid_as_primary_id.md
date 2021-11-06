This assumes the phoenix app is titled App

Update `config/config.exs` to set the primary migration key type
```elixir
config :app,
  ecto_repos: [App.Repo]

config :app, App.Repo,
  migration_primary_key: [type: :binary_id],
  migration_foreign_key: [type: :binary_id]
```

In `lib/app/` create a file named `schema.ex`
```elixir
defmodule Meston.Schema do
  defmacro __using__(_) do
    quote do
      use Ecto.Schema
      @primary_key {:id, :binary_id, autogenerate: true}
      @foreign_key_type :binary_id
    end
  end
end
```

Then in schema files use `App.Schema` instead of `Ecto.Schema`
```elixir
defmodule App.MyContext.MyResource do
  # use Ecto.Schema
  use App.Schema
  import Ecto.Changeset

  ...
```
