Forker
------
[![Build Status](https://secure.travis-ci.org/hasantayyar/forker.png?branch=master)](http://travis-ci.org/hasantayyar/forker)

Forker presents a simple interfacing for forking in PHP.

## Install

    composer require hasantayyar/forker:dev-master

## Getting Started

    <?php
    use Hasantayyar\Forker\Forker;
    $servers = array('machine1.example.com', 'machine2.example.com');
    
    /**
     * Run a shell command on an array of servers using SSH,
     * returning the output and exit code.
     */
    function runCmd($command, $servers) {
        return Forker::map($servers,
        function($index, $server) use ($command) {
            $sshCommand = "ssh $server -c '$command' 2>&1";
            exec($sshCommand, $exitCode, $output);
            return array(
                'output' => implode("\n", $output),
                'exitCode' => $exitCode
            );
        });
    }
    
    $results = runCmd("hostname", $servers);
    print_r($results);
