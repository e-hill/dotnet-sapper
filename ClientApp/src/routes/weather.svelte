<script type="text/javascript">
  let promise = fetchWeatherData();

  async function fetchWeatherData() {
    const baseUrl = window.location.origin;
    const res = await fetch(`${baseUrl}/weatherforecast`);
    const json = await res.json();
    if (res.ok) {
      return json;
    } else {
      throw new Error(text);
    }
  }
</script>

<style>

</style>

<svelte:head>
  <title>Current weather</title>
</svelte:head>

<h1 id="tableLabel">Weather forecast</h1>

<p>This component demonstrates fetching data from the server.</p>

{#await promise}
  <em>Loading...</em>
{:then forecasts}
  <table class="table table-striped" aria-labelledby="tableLabel">
    <thead>
      <tr>
        <th>Date</th>
        <th>Temp. (C)</th>
        <th>Temp. (F)</th>
        <th>Summary</th>
      </tr>
    </thead>
    <tbody>
      {#each forecasts as forecast}
        <tr>
          <td>{forecast.date}</td>
          <td>{forecast.temperatureC}</td>
          <td>{forecast.temperatureF}</td>
          <td>{forecast.summary}</td>
        </tr>
      {/each}
    </tbody>
  </table>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
