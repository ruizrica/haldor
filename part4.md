### Chapter IX: Establishing the Hall of Chronicles - Installing PostgreSQL

Our saga continues as we seek to establish a Hall of Chronicles, a place where every victory and setback of our trading bot is recorded for posterity. This hall will be built upon the sturdy foundations of PostgreSQL, a database as steadfast and reliable as the mightiest of Viking longhouses.

#### Step 1: Installing PostgreSQL

1. **Download PostgreSQL**: Begin your journey at the [official PostgreSQL website](https://www.postgresql.org/download/). Select the version that matches your seafaring vessel's operating system (Windows, macOS, or Linux).

2. **Install PostgreSQL**: Follow the guidance of the runes as you proceed through the installation wizard. You'll be asked to bestow a password upon the default 'postgres' user—a password as strong as the walls of Asgard—and to choose a port for docking your database ship (5432 is the traditional choice).

3. **Verify Installation**: Once the installation process is complete, summon the PostgreSQL command line tool, `psql`, to ensure you can connect to your newly established database realm.

#### Step 2: Crafting the Database

With PostgreSQL now a trusted ally, it's time to create a sacred space within it to store our chronicles.

1. **Open the Gates with `psql`**: Invoke `psql` from your command line, entering the realm as the 'postgres' user.

2. **Found Your Database**:

   ```sql
   CREATE DATABASE crypto_trading_saga;
   ```

   This spell creates a new database, a vast hall where the tales of our trades will be sung.

3. **Erect the Pillars of the Hall**:

   Connect to your new database and begin construction on a table that will stand as a testament to your trading endeavors:

   ```sql
   \c crypto_trading_saga

   CREATE TABLE trades (
     id SERIAL PRIMARY KEY,
     action VARCHAR(10),
     symbol VARCHAR(10),
     quantity NUMERIC,
     price NUMERIC,
     timestamp TIMESTAMP WITHOUT TIME ZONE
   );
   ```

This table, with columns for action, symbol, quantity, price, and timestamp, will serve as the bedrock of our chronicles, holding stories of wealth amassed and opportunities missed.

#### Step 3: Connecting Your Project to PostgreSQL

To ensure our bot can inscribe its saga directly into the Hall of Chronicles, we must forge a link between our project and PostgreSQL. This link is crafted with `pg`, a set of runes that allows Node.js to speak directly to PostgreSQL.

1. **Install `pg`**: Add the PostgreSQL client to your project with a chant at your command line:

   ```shell
   npm install pg
   ```

2. **Forge the Connection**:

   With `pg` now part of your arsenal, set up a connection to your PostgreSQL database. This can be done within your trading function or a dedicated module for database operations:

   ```javascript
   const { Pool } = require('pg');
   const pool = new Pool({
     user: 'postgres',
     host: 'localhost',
     database: 'crypto_trading_saga',
     password: 'yourPasswordHere',
     port: 5432,
   });

   async function recordTradeInPostgres(action, symbol, quantity, price) {
     const query = `
       INSERT INTO trades(action, symbol, quantity, price, timestamp)
       VALUES($1, $2, $3, $4, NOW())
     `;
     await pool.query(query, [action, symbol, quantity, price]);
   }
   ```

In this incantation, replace `'yourPasswordHere'` with the password you bestowed upon the 'postgres' user during the installation rites.

### Chapter IX: Conclusion

With the Hall of Chronicles established and our bot empowered to record its journey, we stand ready to review our saga, learning from past battles to strategize future conquests. This repository of knowledge, safeguarded within PostgreSQL, will guide us as we navigate the treacherous waters of the cryptocurrency markets.

As we conclude this chapter, let us prepare to summon the oracle, Metabase, in our next gathering. With it, we will divine deeper insights from our chronicles, visualizing the path to glory and riches in the markets of Midgard.
