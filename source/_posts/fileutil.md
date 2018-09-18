---
title: 文件处理类
date: 2018-08-28 20:56:00
tags: 
	- 工具 
	- 文件
	 
categories: [Java工具]

---


1.生成文件名，避免文件重复

	public static String getRandomFileName() {
		// 生成随机文件名：当前年月日时分秒+五位随机数（为了在实际项目中防止文件同名而进行的处理）
		int rannum = (int) (r.nextDouble() * (99999 - 10000 + 1)) + 10000; // 获取随机数
		String nowTimeStr = sDateFormat.format(new Date()); // 当前时间
		return nowTimeStr + rannum;
	}

2.删除文件或目录

	public static void deleteFile(String storePath) {
		File file = new File( storePath);
		if (file.exists()) {
			if (file.isDirectory()) {
				File files[] = file.listFiles();
				for (int i = 0; i < files.length; i++) {
					files[i].delete();
				}
			}
			file.delete();
		}
	}

3.读取文件内容到string中

	public static String readFileToStr(String path){
		StringBuffer stringBuffer=new StringBuffer();
		try {
			BufferedReader in = new BufferedReader(new FileReader(path));
		String line=	in.readLine();
		while (line!=null){
			stringBuffer.append(line);
			line=in.readLine();
		}
		in.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		return stringBuffer.toString();
	}

4.读取配置文件内容到map，可通过map读取对应配置

		 public static HashMap<String, String> readFiletoMap(String path) {
	        HashMap<String, String> propeMap = new HashMap<String, String>();
	        String[] tem;
	        String line="";
	        try {
	            BufferedReader in = new BufferedReader(new FileReader(path));
	            line = in.readLine();
	            while (line != null) {
	               tem=line.split("=");
	               if (tem.length>1)
	                propeMap.put(tem[0],tem[1]);
	                line = in.readLine();
	            }
	            in.close();
	        } catch (FileNotFoundException e) {
	            e.printStackTrace();
	        } catch (IOException e) {
	            e.printStackTrace();
	        }
	        return propeMap;
    	}

<center>[Coding Blog](http://kangtian.coding.me)     &nbsp;&nbsp;&nbsp;    [Github Blog  ](http://pankangtian.github.io/) </center>