# 离线下载合并B站视频

```php
<?php
/**
 * B站音频+视频合并输出 
 * @author chenjinle
 * @date 2020/9/22
 */


class Bvideo {

	private $_outDir = 'out/';
	private $_inDir = 'in/';

	public function __construct() {
		$this->_outDir = __DIR__.'/'.$this->_outDir;
		$this->_inDir = __DIR__.'/'.$this->_inDir;
	}


	public function run() {
		if ($handle = opendir($this->_inDir)) {
			while (false !== ($file = readdir($handle))) {
				if ($file == '.' || $file == '..') continue;
				if (!is_dir($this->_inDir.$file)) continue;
				$jsonFile = $this->_inDir.$file.'/entry.json';
				$json = file_get_contents($jsonFile);
				$arr = json_decode($json, true);
				$typeTag = $arr['type_tag'];
				// if ($file != '13') continue;
				$outFile = $this->_outDir.$arr['page_data']['part'].$arr['page_data']['cid'].'.mp4';
				if (strpos($typeTag, 'lua') !== false) {
					$jsonFile = $this->_inDir.$file.'/'.$typeTag.'/index.json';
					$json = file_get_contents($jsonFile);
					$indexArr = json_decode($json, true);
					$cnt = 0;
					if (isset($indexArr['segment_list'])) {
						$cnt = count($indexArr['segment_list']);
						$aFile = array();
						for ($i = 0; $i < $cnt; $i++) {
							$aFile[] = $this->_inDir.$file.'/'.$typeTag.'/'.$i.'.blv';
						}
					} else {
						$aFile = array(
							$this->_inDir.$file.'/'.$typeTag.'/0.blv',
						);
					}
					$aa = $this->encodeBlv($aFile, $outFile);
				} else {
					$aFile = array(
						$this->_inDir.$file.'/'.$typeTag.'/video.m4s',
						$this->_inDir.$file.'/'.$typeTag.'/audio.m4s',
					);
					$aa = $this->encode($aFile, $outFile);
				}
				var_dump($outFile, $aa);
			}
		}
		echo "done!\n";

	}

	/**
	 * 视频输出
	 */
	public function encode($aFile, $outFile) {
		if (empty($aFile) || empty($outFile)) {
			return false;
		}
		$cmd = "ffmpeg";
		foreach ($aFile as $file) {
			$cmd .= sprintf(" -i '%s' ", $file);
		}
		$cmd .= " -c copy '{$outFile}'";
		system($cmd, $flg);
		return $flg;
	}

	/**
	 * blv转mp4
	 */
	public function encodeBlv($aFile, $outFile) {
		if (empty($aFile) || empty($outFile)) {
			return false;
		}
		foreach ($aFile as $idx=>$file) {
			$newOutFile = str_replace('.mp4', '.'.$idx.'.mp4', $outFile);
			$cmd = sprintf("ffmpeg -i '%s' -c copy '%s' ", $file, $newOutFile);
			system($cmd, $flg);
		}
		return $flg;
	}

}




$obj = new Bvideo();
// var_dump(__DIR__, __FILE__);
$obj->run();

```