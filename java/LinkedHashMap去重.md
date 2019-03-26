# 使用LinkedHashMap去重

###### 去重原理
1. ListHashMap 空集合 用于去重和存储去重后的数据  
2. List 一个含有重复数据的集合  

>  
	for循环List集合并将数据存储到map集合中
	如果当前map集合中已经有循环到当前的List的对象 则新建对象 重写数据 并将想要重组的数据重组（比如求和）
	否则直接将对象添加到map中
	最后得到重组后的map数据
	清空List集合
	迭代map数据放入List集合中
	得到重组后（去重）的数据




> 
	package top.txwgoogol.test;
	import org.junit.Test;
	import java.util.ArrayList;
	import java.util.Iterator;
	import java.util.LinkedHashMap;
	import java.util.List;
	import java.util.Map;

	public class RemoveDuplicateUnitTest {

	    @Test
	    public void removeDuplicate() {
	        List<TUnitTest.Goods> goodsList = new ArrayList<>();
	        TUnitTest.Goods goods1 = new TUnitTest.Goods();
	        goods1.setSkuId("10000");
	        goods1.setSkuName("苹果牌-安卓手机");
	        goods1.setSkuCode("not allow");
	        goods1.setQty(2);
	        goodsList.add(goods1);

	        TUnitTest.Goods goods2 = new TUnitTest.Goods();
	        goods2.setSkuId("10000");
	        goods2.setSkuName("苹果牌-安卓手机");
	        goods2.setSkuCode("not allow");
	        goods2.setQty(8);
	        goodsList.add(goods2);

	        TUnitTest.Goods goods3 = new TUnitTest.Goods();
	        goods3.setSkuId("10001");
	        goods3.setSkuName("安卓牌-苹果手机");
	        goods3.setSkuCode("allow");
	        goods3.setQty(1);
	        goodsList.add(goods3);

	        TUnitTest.Goods goods4 = new TUnitTest.Goods();
	        goods4.setSkuId("10001");
	        goods4.setSkuName("安卓牌-苹果手机");
	        goods4.setSkuCode("allow");
	        goods4.setQty(1);
	        goodsList.add(goods4);

	        TUnitTest.Goods goods5 = new TUnitTest.Goods();
	        goods5.setSkuId("10001");
	        goods5.setSkuName("安卓牌-苹果手机");
	        goods5.setSkuCode("allow");
	        goods5.setQty(1);
	        goodsList.add(goods5);

	        TUnitTest.Goods goods6 = new TUnitTest.Goods();
	        goods6.setSkuId("10002");
	        goods6.setSkuName("安卓牌-苹果手机");
	        goods6.setSkuCode("allow");
	        goods6.setQty(2);
	        goodsList.add(goods6);

	        TUnitTest.Goods goods7 = new TUnitTest.Goods();
	        goods7.setSkuId("10003");
	        goods7.setSkuName("安卓牌-苹果手机");
	        goods7.setSkuCode("allow");
	        goods7.setQty(3);
	        goodsList.add(goods7);

	        removeDuplicateAboutListMap(goodsList);

	    }

	    // 编号相同 值合并
	    private void removeDuplicateAboutListMap(List<TUnitTest.Goods> goodsList) {


	        //List<Goods> goodsList = new ArrayList<>();
	        Map<String, TUnitTest.Goods> map = new LinkedHashMap<>();
	        for (TUnitTest.Goods goods : goodsList) {
	            if (map.containsKey(goods.getSkuId())) {


	                TUnitTest.Goods goods1 = new TUnitTest.Goods();
	                goods1.setSkuId(goods.getSkuId());
	                goods1.setSkuName(goods.getSkuName());
	                goods1.setSkuCode(goods.getSkuCode());

	                System.out.println("goods_qty=" + goods.getQty()
	                        + "map_qty=" + map.get(goods.getSkuId()).getQty());
	                goods1.setQty((goods.getQty() + map.get(goods.getSkuId()).getQty()));


	                map.remove(goods.getSkuId());
	                map.put(goods.getSkuId(), goods1);

	            } else {
	                map.put(goods.getSkuId(), goods);
	            }
	        }

	        System.out.println("==========map.size=========" + map.size());

	        goodsList.clear();
	        Iterator<Map.Entry<String, TUnitTest.Goods>> iterator = map.entrySet().iterator();

	        while (iterator.hasNext()) {
	            TUnitTest.Goods goods = new TUnitTest.Goods();
	            Map.Entry<String, TUnitTest.Goods> entry = iterator.next();
	            goods.setSkuId(entry.getValue().getSkuId());
	            goods.setSkuName(entry.getValue().getSkuName());
	            goods.setSkuCode(entry.getValue().getSkuCode());
	            goods.setQty(entry.getValue().getQty());
	            goodsList.add(goods);
	        }

	        for (int i = 0; i < goodsList.size(); i++) {
	            System.out.println("skuId=" + goodsList.get(i).getSkuId()
	                    + " skuName=" + goodsList.get(i).getSkuName()
	                    + " skuCode=" + goodsList.get(i).getSkuCode()
	                    + " qty=" + goodsList.get(i).getQty()
	            );
	        }

	        /*
	        // 如果list中的对像的编号相同就把对像合并，并将数量相加
	        List<Object> list = new ArrayList<>();
	        Map<String, Object> map = new HashMap<>();
	        for(Object obj : list){
	            if(map.containsKey(obj.getNo)){
	                Object o = map.get("obj");
	                o.setNum(o.getNum + obj.getNum);
	                map.put(obj.getNo, o);
	            }else{
	                map.put(obj.getNo, obj);
	            }
	        }
	        */


	    }

	    public static class Goods {

	        private String skuId;
	        private String skuName;
	        private String skuCode;
	        private int qty;

	        public String getSkuId() {
	            return skuId;
	        }

	        public void setSkuId(String skuId) {
	            this.skuId = skuId;
	        }

	        public String getSkuName() {
	            return skuName;
	        }

	        public void setSkuName(String skuName) {
	            this.skuName = skuName;
	        }

	        public String getSkuCode() {
	            return skuCode;
	        }

	        public void setSkuCode(String skuCode) {
	            this.skuCode = skuCode;
	        }

	        public int getQty() {
	            return qty;
	        }

	        public void setQty(int qty) {
	            this.qty = qty;
	        }
	    }

	}
